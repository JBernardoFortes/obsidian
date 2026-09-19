
[[ativ05_self_attention-1.pdf]]

# Tópicos em IA 


Atividade: Prática 2 — Self-Attention  
Grupo 02: ARTUR VINICIUS SILVA SOUSA, JOSE BERNARDO ALVES FORTES, THALYSSON ARAUJO MELO

Referência de implementação: [https://github.com/rasbt/LLMs-from-scratch/tree/main/ch03/01_main-chapter-code](https://github.com/rasbt/LLMs-from-scratch/tree/main/ch03/01_main-chapter-code) (cap. 3), estendido p/ cap. 4 (GPTModel, TransformerBlock) e cap. 5 (GPTDatasetV1, train_model_simple)

# Resumo

Este relatório responde às 6 questões da atividade e documenta as decisões de projeto adotadas para implementar o pipeline completo: (1) quatro variantes de atenção, (2) bloco Transformer, (3) modelo GPT-like com carga de pesos, (4) cálculo de memória, (5) dataset/dataloader em português, (6) pré-treino por 3 épocas com avaliação qualitativa.

  

# Q1. As quatro estratégias do mecanismo de atenção

Todas as implementações recebem x: (B, T, d_in) — B batch, T nº de tokens na janela, d_in dim. de embedding de entrada — e devolvem contexto (B, T, d_out).

## Q1-i) Self-attention sem pesos treináveis (baseline didático)

Objetivo: entender a mecânica pura antes de introduzir parâmetros.

Decisão de projeto: usar produto escalar bruto + softmax, sem projeções e sem escala. É a versão do início do ch03.ipynb.

import torch

import torch.nn.functional as F

# x: (T, d_in) — exemplo com uma sentença, sem batch

torch.manual_seed(123)

x = torch.rand(6, 3)  # 6 tokens, dim 3 (exemplo didático)

# 1. scores brutos

omega = x @ x.T  # (T, T)

# 2. normalização por linha

attn_weights = F.softmax(omega, dim=-1)

# 3. contexto = combinação ponderada das próprias entradas

context = attn_weights @ x  # (T, d_in)

  

Resposta / observação: funciona como média ponderada por similaridade, mas tem 3 limitações que justificam Q1-ii: (a) sem parâmetros, não aprende o *que* comparar; (b) sem escala 1/sqrt(d), softmax satura em dims altas; (c) sem causalidade, token futuro vaza para o passado.

## Q1-ii) Self-attention com pesos treináveis (Wq, Wk, Wv)

import torch.nn as nn

class SelfAttention_v2(nn.Module):

    def __init__(self, d_in, d_out, qkv_bias=False):

        super().__init__()

        self.W_query = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.W_key   = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.W_value = nn.Linear(d_in, d_out, bias=qkv_bias)

    def forward(self, x):  # x: (B, T, d_in)

        K = self.W_key(x)

        Q = self.W_query(x)

        V = self.W_value(x)

        attn_scores = Q @ K.transpose(-2, -1)  # (B, T, T)

        attn_weights = torch.softmax(attn_scores / K.shape[-1]**0.5, dim=-1)

        return attn_weights @ V  # (B, T, d_out)

  

## Q1-iii) Causal attention (masked) + dropout mask

Por que causal? Modelagem autoregressiva (P(x_t | x_<t)) exige que a posição t nunca veja >t. Sem máscara o modelo "cola" na avaliação de next-token.

Decisões de projeto (idênticas ao `CausalAttention` do rasbt):

- register_buffer("mask", torch.triu(torch.ones(C, C), diagonal=1)) — matriz triangular superior, registrada como buffer (não-parâmetro, mas vai p/ GPU com .to(device)).
    
- Truncar máscara para num_tokens real (mask.bool()[:T, :T]) para suportar T < context_length na inferência.
    
- masked_fill_(mask_bool, -torch.inf) antes do softmax → pesos futuros = 0.
    
- nn.Dropout(dropout) após softmax (dropout mask sobre attn_weights), com dropout=0.1 no GPT e 0.2 no dataloader da Q5 (ver Q5).
    

class CausalAttention(nn.Module):

    def __init__(self, d_in, d_out, context_length, dropout, qkv_bias=False):

        super().__init__()

        self.W_query = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.W_key   = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.W_value = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.dropout = nn.Dropout(dropout)

        self.register_buffer(

            "mask",

            torch.triu(torch.ones(context_length, context_length), diagonal=1)

        )

    def forward(self, x):

        B, T, _ = x.shape

        K = self.W_key(x); Q = self.W_query(x); V = self.W_value(x)

        attn_scores = Q @ K.transpose(-2, -1)

        mask_bool = self.mask.bool()[:T, :T]

        attn_scores.masked_fill_(mask_bool, -torch.inf)

        attn_weights = torch.softmax(attn_scores / K.shape[-1]**0.5, dim=-1)

        attn_weights = self.dropout(attn_weights)

        return attn_weights @ V

  

Verificado em teste real (torch CPU, `dropout=0.0` em eval): peso máximo atribuído a posições futuras = 0.0 (máscara triu(diagonal=1) + masked_fill(-inf) antes do softmax); MHA com T=10 < context_length=32 executa sem erro (truncamento mask[:T,:T]); GPT tiny (vocab 50257, emb 64, 1 camada, 4 heads, ctx 256, drop 0.2) devolve logits (4, 256, 50257); .numel() do tiny = 6 499 200 total − 3 216 448 tied = 3 282 752 únicos (~12,5 MB fp32). Em treino usar model.train() (dropout ativo); em geração/validação, model.eval() — senão a saída fica não-determinística.

## Q1-iv) Multi-head attention

Por que multi-head? Uma única cabeça aprende um tipo de relação (ex.: sintática). h cabeças em subespaços head_dim = d_out // h permitem relações em paralelo (sintaxe + correferência + posição).

Decisão de projeto: implementação exata de previous_chapters.py / gpt.py do rasbt (também usada na Q2/Q3):

class MultiHeadAttention(nn.Module):

    def __init__(self, d_in, d_out, context_length, dropout, num_heads, qkv_bias=False):

        super().__init__()

        assert d_out % num_heads == 0, "d_out deve ser divisível por num_heads"

        self.d_out = d_out

        self.num_heads = num_heads

        self.head_dim = d_out // num_heads

        self.W_query = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.W_key   = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.W_value = nn.Linear(d_in, d_out, bias=qkv_bias)

        self.out_proj = nn.Linear(d_out, d_out)  # mistura das cabeças

        self.dropout = nn.Dropout(dropout)

        self.register_buffer(

            "mask", torch.triu(torch.ones(context_length, context_length), diagonal=1)

        )

    def forward(self, x):

        B, T, _ = x.shape

        K = self.W_key(x).view(B, T, self.num_heads, self.head_dim).transpose(1, 2)

        Q = self.W_query(x).view(B, T, self.num_heads, self.head_dim).transpose(1, 2)

        V = self.W_value(x).view(B, T, self.num_heads, self.head_dim).transpose(1, 2)

        # Q,K,V: (B, h, T, head_dim)

        attn_scores = Q @ K.transpose(2, 3)

        attn_scores.masked_fill_(self.mask.bool()[:T, :T], -torch.inf)

        attn_weights = torch.softmax(attn_scores / K.shape[-1]**0.5, dim=-1)

        attn_weights = self.dropout(attn_weights)

        context = (attn_weights @ V).transpose(1, 2)  # (B, T, h, head_dim)

        context = context.contiguous().view(B, T, self.d_out)

        return self.out_proj(context)

  

Configuração (GPT-124M): emb_dim=768, num_heads=12 → head_dim=64, context_length=1024 (256 na Q5/Q6), dropout=0.1. O out_proj mistura as cabeças — sem ele elas nunca interagem.

  

# Q2. Bloco Transformer

Decisão de projeto: ordem pré-norm + residual (norm → att/ff → dropout → + shortcut), como no rasbt cap. 4 / GPT-2. Pré-norm estabiliza 12 camadas; 

Componentes:

|   |   |   |
|---|---|---|
|Componente|Escolha|Justificativa|
|`LayerNorm`|`eps=1e-5`, `scale`/`shift` aprendidos|Normaliza por token `(B,T,C)` sem depender do batch; `scale/shift` recuperam expressividade|
|`FeedForward`|`Linear(C→4C) → GELU → Linear(4C→C)`|Expansão 4× padrão GPT; GELU aproximada por `tanh` (fórmula do GPT-2) dá curvatura suave, melhor que ReLU em LM|
|Dropout shortcut|`nn.Dropout(drop_rate)` após att e após FF|Regularização residual; `0.1` no modelo, `0.2` no embedding/dataloader da Q5|
|Residual|`x + shortcut` nos dois sub-blocos|Permite treinar 12+ camadas (fluxo de gradiente)|

  

class LayerNorm(nn.Module):

    def __init__(self, emb_dim):

        super().__init__()

        self.eps = 1e-5

        self.scale = nn.Parameter(torch.ones(emb_dim))

        self.shift = nn.Parameter(torch.zeros(emb_dim))

    def forward(self, x):

        mean = x.mean(dim=-1, keepdim=True)

        var = x.var(dim=-1, keepdim=True, unbiased=False)

        return self.scale * (x - mean) / torch.sqrt(var + self.eps) + self.shift

class GELU(nn.Module):

    def forward(self, x):

        return 0.5 * x * (1 + torch.tanh(

            torch.sqrt(torch.tensor(2.0 / torch.pi)) * (x + 0.044715 * torch.pow(x, 3))

        ))

class FeedForward(nn.Module):

    def __init__(self, cfg):

        super().__init__()

        self.layers = nn.Sequential(

            nn.Linear(cfg["emb_dim"], 4 * cfg["emb_dim"]),

            GELU(),

            nn.Linear(4 * cfg["emb_dim"], cfg["emb_dim"]),

        )

    def forward(self, x):

        return self.layers(x)

class TransformerBlock(nn.Module):

    def __init__(self, cfg):

        super().__init__()

        self.att = MultiHeadAttention(

            d_in=cfg["emb_dim"], d_out=cfg["emb_dim"],

            context_length=cfg["context_length"],

            num_heads=cfg["n_heads"],

            dropout=cfg["drop_rate"], qkv_bias=cfg["qkv_bias"])

        self.ff = FeedForward(cfg)

        self.norm1 = LayerNorm(cfg["emb_dim"])

        self.norm2 = LayerNorm(cfg["emb_dim"])

        self.drop_shortcut = nn.Dropout(cfg["drop_rate"])

    def forward(self, x):

        shortcut = x

        x = self.norm1(x); x = self.att(x)

        x = self.drop_shortcut(x); x = x + shortcut

        shortcut = x

        x = self.norm2(x); x = self.ff(x)

        x = self.drop_shortcut(x); x = x + shortcut

        return x

# Q3. Modelo GPT-like + carga de pesos

## 3.1 Codificação do modelo

Decisão de projeto: GPTModel idêntico a gpt.py (cap. 4), para que load_state_dict de pesos GPT-2 OpenAI funcione sem remapeamento além de transposição.

class GPTModel(nn.Module):

    def __init__(self, cfg):

        super().__init__()

        self.tok_emb = nn.Embedding(cfg["vocab_size"], cfg["emb_dim"])

        self.pos_emb = nn.Embedding(cfg["context_length"], cfg["emb_dim"])

        self.drop_emb = nn.Dropout(cfg["drop_rate"])

        self.trf_blocks = nn.Sequential(*[TransformerBlock(cfg) for _ in range(cfg["n_layers"])])

        self.final_norm = LayerNorm(cfg["emb_dim"])

        self.out_head = nn.Linear(cfg["emb_dim"], cfg["vocab_size"], bias=False)

    def forward(self, in_idx):  # (B, T)

        B, T = in_idx.shape

        x = self.tok_emb(in_idx) + self.pos_emb(torch.arange(T, device=in_idx.device))

        x = self.drop_emb(x)

        x = self.trf_blocks(x)

        x = self.final_norm(x)

        return self.out_head(x)  # logits (B, T, vocab)

  

Configuração padrão 124M:

GPT_CONFIG_124M = {

    "vocab_size": 50257, "context_length": 1024,

    "emb_dim": 768, "n_heads": 12, "n_layers": 12,

    "drop_rate": 0.1, "qkv_bias": False

}

  

pos_emb aprendido e out_head sem bias por fidelidade ao checkpoint GPT-2 (wpe, sem bias na projeção final).

## 3.2 Carga de pesos e verificação de topologia

- Baixar com gpt_download.py (cap. 5) ou load_gpt2_params_from_tensorflow — pesos vêm em formato TF (conv1D transposta).
    
- Função assign(left, right): verifica left.shape == right.shape, transpõe se left.shape == right.T.shape, senão erro explícito.
    
- Mapeamento: wte → tok_emb, wpe → pos_emb, blocks.h.{i}.attn.c_attn/c_proj → W_query/key/value + out_proj (é preciso fatiar c_attn em Q/K/V), mlp.c_fc/c_proj → FeedForward, ln_1/ln_2/ln_f → LayerNorm (scale/shift), wte (reuso) → out_head se weight tying.
    
- Verificação de topologia: comparar cfg usado na construção com o dicionário do checkpoint (n_layers, n_heads, emb_dim, context_length, vocab_size). Se divergir, não carregar — abortar com mensagem. Teste incluído em tests.py do rasbt.
    

Decisão de projeto: manter qkv_bias=False e emb_dim % n_heads == 0; qualquer desvio quebra o assign. Em código próprio, imprimir model.numel() por bloco para auditoria antes/depois da carga.

Geração (sanity check pós-carga):

def generate_text_simple(model, idx, max_new_tokens, context_size):

    for _ in range(max_new_tokens):

        idx_cond = idx[:, -context_size:]

        with torch.no_grad():

            logits = model(idx_cond)

        idx_next = torch.argmax(logits[:, -1, :], dim=-1, keepdim=True)

        idx = torch.cat((idx, idx_next), dim=1)

    return idx

  
  

# Q4. Requisitos de memória (`.numel()` + weight tying)

## 4.1 Função

def gpt_memory_report(model: nn.Module, weight_tying: bool = True, bytes_per_param: int = 4):

    total = sum(p.numel() for p in model.parameters())  # == model.numel() p/ nn.Module

    tied = 0

    if weight_tying:

        # GPT-2 reusa wte em out_head: descontar uma cópia

        tied = model.tok_emb.weight.numel()  # vocab_size * emb_dim

        total_unique = total - tied

    else:

        total_unique = total

    mem_mb = total_unique * bytes_per_param / (1024 ** 2)

    return {"total_numel": total, "unique_params": total_unique,

            "tied_params": tied, "mem_MB_fp32": mem_mb,

            "mem_MB_fp16": total_unique * 2 / (1024**2),

            "mem_MB_int8": total_unique * 1 / (1024**2)}

  

Decisões: (a) usar .numel() somado — inclui scale/shift da LayerNorm e biases (quando houver); (b) subtrair vocab × emb_dim quando weight_tying=True (caso GPT-2); (c) reportar fp32 (treino de referência), fp16 e int8 para inferência; (d) considerar só pesos — ativações/otimizador (AdamW ~2× pesos + gradientes) são custo adicional em treino.

## 4.2 Estimativas (pesos únicos, fp32)

|   |   |   |   |
|---|---|---|---|
|Modelo|Parâmetros únicos aprox.|Memória fp32|Memória fp16|
|GPT-2 small (124M)|~124 M (163,0 M brutos − 38,6 M tied*)|~474 MB|~237 MB|
|GPT-2 medium (355M)|~355 M|~1 354 MB (~1,32 GB)|~677 MB|
|GPT-2 large (774M)|~774 M|~2 953 MB (~2,88 GB)|~1 476 MB|
|GPT-2 XL (1,5B)|~1 558 M|~5 943 MB (~5,80 GB)|~2 972 MB|

  

* 50257 × 768 = 38.597.376. O .numel() do GPTModel ingênuo retorna ~163 M; o número "124M" oficial já desconta o tying. Esse é o erro mais comum na questão — não descontar conta ~38,6 M a mais.

Valores calculados por params × bytes / 1024². Podem variar ±1% por inclusão de bias (qkv_bias) conforme cfg.

  

# Q5. Dados em português — Dataset e DataLoader

Decisão de corpus: usar os .txt de data/processed/text/ do projeto pipeline-BDTD (teses/dissertações BDTD em Computação/Informática/Informação, já limpos e anonimizados), concatenados com delimitador <|endoftext|> entre documentos. Tokenizador fixo: tiktoken.get_encoding("gpt2") (vocab 50257) — não treinar BPE novo, para manter compatibilidade com pesos da Q3.

Medido em 2026-09-18 (teste real, `tiktoken` 0.14 + `GPTDatasetV1` do rasbt):

|   |   |
|---|---|
|Métrica|Valor|
|Documentos (`data/processed/text/*.txt`)|33|
|Parágrafos totais / média por doc|86 541 / 2 622,5|
|Palavras por doc (média / mín / máx)|27 875 / 1 621 / 81 873|
|Caracteres totais|6 175 458|
|Tokens GPT-2 BPE totais|2 302 465|
|`vocab_size` confirmado|50 257|
|Roundtrip `decode(encode(x))==x`|OK|
|`Raimundo Moura` → tokens|`[49, 1385, 41204, 49902, 430]`|
|Batches treino/val (256/128/4, split 90/10)|4 042 / 454|
|`input.shape == target.shape`|`(4, 256)` OK|
|`target[:, :-1] == input[:, 1:]` (shift)|OK|

  

 Divergência: a Ativ. 1 indica [49, 1385, 41204, 49902, 403]; o tiktoken atual gera 430 no último token (Moura). Diferença atribuída à versão do BPE/merges — reportada aqui como observada, sem mascarar.

Parâmetros exigidos pela questão — todos atendidos em create_dataloader_v1:

from torch.utils.data import Dataset, DataLoader

import tiktoken, torch

class GPTDatasetV1(Dataset):

    def __init__(self, txt, tokenizer, max_length, stride):

        self.input_ids, self.target_ids = [], []

        ids = tokenizer.encode(txt, allowed_special={"<|endoftext|>"})

        for i in range(0, len(ids) - max_length, stride):

            self.input_ids.append(torch.tensor(ids[i:i+max_length]))

            self.target_ids.append(torch.tensor(ids[i+1:i+max_length+1]))

    def __len__(self): return len(self.input_ids)

    def __getitem__(self, idx): return self.input_ids[idx], self.target_ids[idx]

def create_dataloader_v1(txt, batch_size=4, max_length=256, stride=128,

                         shuffle=True, drop_last=True, num_workers=0):

    tok = tiktoken.get_encoding("gpt2")

    ds = GPTDatasetV1(txt, tok, max_length, stride)

    return DataLoader(ds, batch_size=batch_size, shuffle=shuffle,

                      drop_last=drop_last, num_workers=num_workers)

  

Instanciação conforme o enunciado:

with open("teses_dissertacoes_pt.txt", encoding="utf-8") as f:

    text_data = f.read()

split = int(0.9 * len(text_data))

train_loader = create_dataloader_v1(text_data[:split],

    batch_size=4, max_length=256, stride=128, shuffle=True, drop_last=True)

val_loader = create_dataloader_v1(text_data[split:],

    batch_size=4, max_length=256, stride=128, shuffle=False, drop_last=False)

# dropout de 20%: cfg["drop_rate"] = 0.2 no modelo desta fase

GPT_CONFIG_PT = {**GPT_CONFIG_124M, "context_length": 256, "drop_rate": 0.2}

  

# Q6. Pré-treino por 3 épocas

## 6.1 Loop de treino (cap. 5, adaptado)

device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

model = GPTModel(GPT_CONFIG_PT).to(device)

optimizer = torch.optim.AdamW(model.parameters(), lr=5e-4, weight_decay=0.1)

tokenizer = tiktoken.get_encoding("gpt2")

def calc_loss_batch(inp, tgt, model, device):

    inp, tgt = inp.to(device), tgt.to(device)

    logits = model(inp)

    return torch.nn.functional.cross_entropy(logits.flatten(0, 1), tgt.flatten())

# train_model_simple: epoch loop, eval a cada eval_freq, generate_and_print_sample ao fim de cada época

# num_epochs=3, eval_freq=5, eval_iter=1, start_context="A Universidade Federal do Piauí"

  

Hiperparâmetros: lr=5e-4, weight_decay=0.1, AdamW, seed=123. context_length=256 no treino (não 1024) por VRAM.

Resultado esperado (padrão observado no livro e reprodutível): train_loss cai de ~9–10 → ~3–5 em 3 épocas em corpus pequeno; val_loss cai menos e pode estagnar na época 3 (sinal de overfit inicial — aceitável para a atividade

# Referências

- Raschka, S. *Build a Large Language Model From Scratch*. Manning. Repo: rasbt/LLMs-from-scratch (cap. 3–5).
    
- Vaswani et al. (2017). *Attention Is All You Need*.
    
- Radford et al. (2019). *Language Models are Unsupervised Multitask Learners* (GPT-2).
    
- Documentos da disciplina: ativ05_self_attention.pdf, ativ04_tokenizador-1.pdf.



[[Topicos em Inteligencia Artificial]]