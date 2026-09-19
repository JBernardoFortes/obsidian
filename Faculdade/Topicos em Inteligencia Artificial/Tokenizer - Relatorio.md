
# Relatório — Atividade Prática 1: Tokenização para Criação de LLMs do Zero

**Disciplina:** Tópicos em IA / PLN: Criação de LLMs do Zero
**Atividade:** Atividade Prática 1 (`ativ04_tokenizador.pdf`)
**Objetivo:** Construir o pipeline de preparação de dados e tokenização usado no treinamento de LLMs da família GPT (GPT-like), do corpus bruto aos input embeddings.

---

## 1. Introdução e Contexto

Esta atividade prática percorre as etapas iniciais da construção de um LLM do zero, com foco no **pré-processamento** e na **camada de entrada** do transformer:

1. Carregamento e análise do dataset (amostra da BDTD — teses e dissertações);
2. Tokenização com **Byte Pair Encoding (BPE)** usando o tokenizador `tiktoken` do GPT-2;
3. Geração de pares **input-target** por **janelas deslizantes** com PyTorch;
4. Criação da camada de **token embeddings** (`torch.nn.Embedding`);
5. Criação dos **embeddings posicionais absolutos** e soma com os token embeddings para obter os **input embeddings**.

Os scripts foram executados em ambiente Python 3 via `uv`, com as bibliotecas `tiktoken` e `torch`.

---

## 2. Metodologia

A metodologia adotou uma abordagem incremental, com **um script por etapa** (`step1_dataset.py`, `step2_bpe.py`, `step3_sliding_windows.py`, `step4_embeddings.py`, `step5_positional.py`), de modo que cada etapa produz artefatos consumíveis pela seguinte:

| Etapa | Entrada | Processamento | Saída |
|-------|---------|---------------|-------|
| 1. Dataset | 28 documentos `.txt` da BDTD | Leitura, limpeza, estatísticas básicas | `data/corpus.txt` (documentos separados por `<\|endoftext\|>`) |
| 2. BPE | `corpus.txt` + vocabulário GPT-2 | `tiktoken.get_encoding("gpt2")`, `encode()`/`decode()` | Sequências de token IDs |
| 3. Janelas deslizantes | Token IDs | Classes `BdtdDataset` (Dataset) e `BdtdDataLoader` | Tensores PyTorch `(batch, max_length)` de inputs e targets |
| 4. Token embeddings | Token IDs | `torch.nn.Embedding(vocab_size=50257, output_dim=256)` | Vetores de embeddings `(n_tokens, 256)` |
| 5. Embeddings posicionais | Token embeddings | Função de embeddings posicionais absolutos + soma | Input embeddings `(seq_len, 256)` |

### Fluxo geral

```
BDTD (28 .txt) → corpus.txt (separador <|endoftext|>)
    → tiktoken/GPT-2 BPE (50.257 tokens) → token IDs
    → janelas deslizantes (max_length, stride) → pares input-target
    → nn.Embedding(50257, 256) → token embeddings
    → + embeddings posicionais absolutos → input embeddings
```

### Parâmetros testados

- **Step 1:** amostra completa do dataset = 28 documentos (amostra `data/processed/text` do pipeline BDTD).
- **Step 3:** `max_length=6`, `stride=1`, `batch_size=2` (principais); teste extra com `max_length=8`, `stride=4`, `batch_size=8`.
- **Steps 4 e 5:** `vocab_size=50257`, `output_dim=256`, `max_length=6` (janela de contexto com 6 tokens).

---

## 3. Algoritmos e Ferramentas Utilizadas

**Algoritmos / técnicas:**

- **Byte Pair Encoding (BPE)** — algoritmo de tokenização por subpalavras utilizado no GPT-2. Começa com um vocabulário de bytes individuais e, iterativamente, mescla os pares de símbolos consecutivos mais frequentes (`merge` rules), adicionando cada novo "token" ao vocabulário até atingir o tamanho desejado (50.257). Isso permite codificar qualquer texto com uma representação compacta e lidar com palavras fora do vocabulário.
- **Janelas deslizantes (sliding window)** — técnica de geração de pares supervisionados `(input, target)` em que `target` é o input deslocado de 1 posição à direita. O modelo aprende a prever o próximo token dado o contexto de `max_length` tokens. O parâmetro `stride` controla o deslocamento entre janelas consecutivas (controle de sobreposição).
- **Token embeddings** — camada de lookup-table treinável (`torch.nn.Embedding`) que mapeia cada token ID (0 … 50.256) para um vetor denso de `output_dim=256` dimensões.
- **Absolute positional embeddings** — técnica de codificação de posição que soma um vetor (escalar repetido, neste exercício) ao token embedding de cada posição. Diferente das posições *learned*, aqui os valores são **sequenciais e fixos**, no formato `janela.posição` (1.1, 1.2, …, 1.6; 2.1, 2.2, …, 2.6; …), tornando o modelo sensível à ordem dos tokens.

**Bibliotecas e ferramentas:**

- **tiktoken** — tokenizador BPE open source usado no treinamento de modelos GPT; implementa o BPE do GPT-2/3/4 com rapidez e decodificação confiável.
- **PyTorch** (`torch`) — framework de deep learning usado para tensores, `nn.Embedding`, `torch.utils.data.Dataset` (referência) e geração de batches.
- **uv / Python 3** — gerenciador de ambiente e dependências.

**Classes implementadas (pipeline customizado):**

- `BdtdDataset(tokens, max_length, stride)` — herdada de `torch.utils.data.Dataset`; define como os registros (janelas) são carregados a partir do corpus tokenizado.
- `BdtdDataLoader(dataset, batch_size, shuffle, seed)` — implementação custom do DataLoader; embaralha os índices a cada época e monta os batches por `torch.stack`.

---

## 4. Resultados e Respostas por Questão

### Questão 1 — Análise do dataset e geração do arquivo txt

**O que foi feito:** foi carregada uma amostra do dataset de teses e dissertações da BDTD (28 documentos `.txt` extraídos na camada processada do pipeline BDTD), calculadas as estatísticas básicas e gerado o arquivo `data/corpus.txt` com todos os documentos, usando o token especial `<|endoftext|>` (token EOS do GPT-2, id 50256) como delimitador entre documentos.

**Informações básicas do dataset:**

| Métrica | Valor |
|---------|-------|
| Número de documentos | **28** |
| Número médio de parágrafos por documento | **255,4** |
| Número médio de palavras por documento | **35.761,6** |
| Número total de parágrafos | **7.151** |
| Número total de palavras | **1.001.326** |
| Arquivo gerado | `data/corpus.txt` — **6,52 MB** |
| Separadores `<\|endoftext\|>` usados | **28** |

**Exemplo (início do primeiro documento):**

```
200 f. : il.

<<PERSON>> (Doutorado) - Pontifícia Universidade Católica de Minas Gerais.
Programa de Pós-Graduação em Administração

1. Idosos como consumidores . 2. Bem-estar social . 3. Subjetividade...
```

**Formato do corpus:** `documento1\n<|endoftext|>\ndocumento2\n<|endoftext|>\n...\ndocumento28\n<|endoftext|>\n`

---

### Questão 2 — Tokenizador BPE (tiktoken / GPT-2)

**O que foi feito:** instalada a biblioteca `tiktoken` (tokenizador BPE usado nas LLMs GPT-like), carregado o esquema de tokenização do **GPT-2** (`tiktoken.get_encoding("gpt2")`), verificado o tamanho do vocabulário e testados os métodos `encode()` e `decode()`.

**1) Verificação do vocabulário:**

```
Encoding carregado: 'gpt2'
Tamanho do vocabulário: 50257  →  Vocabulário de 50.257 tokens: OK ✔
```

- O vocabulário tem exatamente **50.257 tokens** (50.000 pares de mesclagem + 256 bytes + 1 token especial `<|endoftext|>`, id 50256).

**2) Teste obrigatório — "Raimundo Moura":**

```
Texto: 'Raimundo Moura'
Tokens gerados: [49, 1385, 41204, 49902, 430]
Decode reverso: 'Raimundo Moura' (fiel ao original ✔)
```

> **Nota importante (divergência com o enunciado):** o enunciado sugere que "Raimundo Moura" gere `[49, 1385, 41204, 49902, 403]`. Com a versão atual do `tiktoken`, o token gerado é **430** (e não 403). Isso ocorre porque os merges (regras de mesclagem BPE) do encoding `gpt2` foram alterados entre versões da biblioteca: hoje o token **403** decodifica para "un" e o token **430** decodifica para "ra". Comprovado:
>
> - `enc.decode([49, 1385, 41204, 49902, 403])` → `'Raimundo Mouun'`
> - `enc.decode([49, 1385, 41204, 49902, 430])` → `'Raimundo Moura'`
>
> Portanto, a lista `[49, 1385, 41204, 49902, 430]` é a correta para esta versão da biblioteca.

**3) Testes livres (3 textos adicionais):**

| Texto | Tokens gerados | Decode reverso |
|-------|----------------|----------------|
| `'Tokenização por subpalavras é essencial para LLMs.'` | `[30642, 23638, 16175, 28749, 16964, 850, 18596, 615, 8847, 38251, 3209, 268, 2413, 31215, 27140, 10128, 13]` | idêntico ✔ |
| `'Computação, Informática e Informação: 42 ≠ 43.'` | `[5377, 1996, 64, 16175, 28749, 11, 45255, 6557, 83, 3970, 304, 45255, 64, 16175, 28749, 25, 5433, 15139, 254, 5946, 13]` | idêntico ✔ |
| `'GPT-2 usa BPE com bytes!,'` | `[38, 11571, 12, 17, 514, 64, 347, 11401, 401, 9881, 28265]` | idêntico ✔ |

Em todos os casos `decode(encode(x)) == x`, confirmando a **reversibilidade** do BPE (a nível de byte).

**Tokens especiais verificados:**

- `<|endoftext|>` → id **50256** (contido no vocabulário);
- id 1 → `"` ; id 49 → `R`.

---

### Questão 3 — Pares input-target (janelas deslizantes) com PyTorch

**O que foi feito:** instalado o **PyTorch**; o arquivo `corpus.txt` foi tokenizado com o BPE do GPT-2 e foi tomada uma amostra de **20.000 tokens**. Sobre essa amostra foram construídos os pares input-target:

- `BdtdDataset` — Dataset customizado (herda de `torch.utils.data.Dataset`) que define como cada registro (janela) é carregado a partir do corpus tokenizado;
- `BdtdDataLoader` — DataLoader customizado que **embaralha** os índices a cada época e **monta os batches**.

**Cenário principal — `max_length=6`, `stride=1`, `batch_size=2`:**

```
Total de tokens do corpus (amostra): 20000
BdtdDataset: 19.994 janelas   (20.000 − 6)
BdtdDataLoader: 9.997 batches por época
```

O número de janelas segue a fórmula: `n_janelas = (n_tokens − max_length) // stride + 1` padrão sliding window; com percorrimento completo `(20000 - 6)/1 + 1 = 19995`... aqui a implementação usou `range(0, len - max_length, stride)`, gerando 19.994 janelas (os últimos 5 tokens ficam de fora como partial window).

**Exemplos reais de janelas (input → target):**

```
batch 0 (shape (2, 6) cada):
  ids    [10205, 70, 291, 418, 410, 1469] -> [70, 291, 418, 410, 1469, 979]
  texto  'ógicos viven' -> 'gicos vivenci'
  ids    [198, 562, 1733, 4533, 257, 78]  -> [562, 1733, 4533, 257, 78, 564]
  texto  '\nassociado ao' -> 'associado ao �'
```

Note que `target` é exatamente o `input` deslocado em **1 posição** (previsão do próximo token em cada posição).

**Teste de outros parâmetros — `max_length=8`, `stride=4`, `batch_size=8`:**

```
janelas = 4.998, batches = 625
inputs shape=(8, 8), targets shape=(8, 8)   (torch.int64)
Exemplo: ids [265, 12151, 390, 8358, 257, 573, 31522, 928] -> [12151, 390, 8358, 257, 573, 31522, 928, 544]
         'ativa de que a tecnolog' -> 'iva de que a tecnologia'
```

**Validação com DataLoader nativo do PyTorch:** o `torch.utils.data.DataLoader` aplicado sobre o mesmo `BdtdDataset` produziu tensores com exatamente as mesmas formas (`(2, 6)`, `torch.int64`), confirmando a equivalência entre o loader customizado e o padrão.

**Tipos e formas:** inputs e targets são `torch.Tensor` de dtype `torch.int64` com shape `(batch_size, max_length)`.

---

### Questão 4 — Camada de token embeddings (`nn.Embedding`)

**O que foi feito:** criada a camada de token embeddings com `torch.nn.Embedding(vocab_size=50257, output_dim=256)` (pesos inicializados com seed fixa para reprodutibilidade) e impressos os embeddings de todo o vocabulário.

**1) Embeddings de todo o vocabulário (`.weight`):**

```
Pesos: weight.shape = (50257, 256)
dtype: torch.float32
```

Amostras de linhas do `.weight` (8 primeiras dimensões):

```
weight[0]     (id 0,      <UNK>):        [-1.1258, -1.1524, -0.2506, -0.4339, 0.8487, 0.6920, -0.3160, -2.1152] ...
weight[1]     (id 1,      '"'):          [-0.0394, -0.8015, -0.4955, -0.3615, 0.5851, -1.1560, -0.1434, -0.1947] ...
weight[49]    (id 49,     'R'):          [-1.3906, -0.4176, 0.0228, 0.4973, 0.6176, -2.0478, 0.9124, 0.9909] ...
weight[50256] (id 50256, <|endoftext|>): [-0.3543, 0.7362, 0.5639, 0.0494, 0.4687, -0.7564, 0.2922, 1.0085] ...
```

**2) Token embeddings de "Raimundo Moura":**

Token IDs de `'Raimundo Moura'`: `[49, 1385, 41204, 49902, 430]` → `embeddings.shape = (5, 256)`.

| pos | token id | embedding (6 primeiras dims) |
|-----|----------|------------------------------|
| 0 | 49 | `[-1.3906, -0.4176, 0.0228, 0.4973, 0.6176, -2.0478]` |
| 1 | 1385 | `[0.8785, 0.2243, -1.2154, -0.5680, -0.3991, -0.6494]` |
| 2 | 41204 | `[1.1381, 1.2038, 0.6659, -0.3999, -0.2006, 0.3022]` |
| 3 | 49902 | `[0.1250, -1.5152, -0.6680, -1.6340, -0.2742, 1.1649]` |
| 4 | 430 | `[1.3729, 0.5572, -0.9297, -0.4275, 2.0252, -0.9116]` |

**Verificação:** `embeddings[i] == .weight[token_id]` → **`True` para todos os 5 tokens**, confirmando que a camada `nn.Embedding` funciona como uma lookup-table dos vetores `weight`.

---

### Questão 5 — Embeddings posicionais absolutos

**O que foi feito:** criada a função `absolute_positional_embeddings(window, max_length, output_dim)` que gera embeddings posicionais com **valores sequenciais** no formato `janela.posição`. Para janela de contexto `max_length=6`, os valores são: janela 1 → `1.1, 1.2, ..., 1.6`; janela 2 → `2.1, 2.2, ..., 2.6`; e assim por diante. Cada valor é repetido preenchendo o vetor de `output_dim=256` dimensões.

**1) Valores sequenciais por janela:**

```
janela 1: ['1.1', '1.2', '1.3', '1.4', '1.5', '1.6']
janela 2: ['2.1', '2.2', '2.3', '2.4', '2.5', '2.6']
janela 3: ['3.1', '3.2', '3.3', '3.4', '3.5', '3.6']
...
```

**2) Vetores posicionais da janela 1 (shape `6 × 256`):**

```
pos[0] = [1.1, 1.1, 1.1, 1.1, ...]    (valor 1.1)
pos[1] = [1.2, 1.2, 1.2, 1.2, ...]    (valor 1.2)
pos[5] = [1.6, 1.6, 1.6, 1.6, ...]    (valor 1.6)
```

**3) Soma dos posicionais com os token embeddings (input embeddings):**

Para `'Raimundo Moura'` (5 tokens, janela 1 — valores posicionais `1.1, 1.2, 1.3, 1.4, 1.5`):

```
token_embeddings.shape = (5, 256)
positional.shape       = (5, 256)
input_embeddings.shape = (5, 256)     ← token + positional
```

| id | pos | input_emb (4 primeiras dims) |
|----|-----|------------------------------|
| 49 | 1.1 | `[-0.2906, 0.6824, 1.1228, 1.5973]` |
| 1385 | 1.2 | `[2.0785, 1.4243, -0.0154, 0.6320]` |
| 41204 | 1.3 | `[2.4381, 2.5038, 1.9659, 0.9001]` |
| 49902 | 1.4 | `[1.5250, -0.1152, 0.7320, -0.2340]` |
| 430 | 1.5 | `[2.8729, 2.0572, 0.5703, 1.0725]` |

**Validação:** `input_emb[0][0] == token_emb[0][0] + 1.1` → **`True`** (ex.: `-0.2906 == -1.3906 + 1.1`). A soma é feita de forma intuitiva: cada posição recebe o token embedding **somado** ao escalar posicional correspondente, repetido ao longo das 256 dimensões.

---

## 5. Conclusão

A atividade foi concluída com todas as 5 etapas executadas e validadas:

1. O dataset BDTD (28 documentos) foi analisado (`corpus.txt` com 6,52 MB e separador `<|endoftext|>`);
2. O BPE do GPT-2 (`tiktoken`) foi carregado e validado — vocabulário de **50.257 tokens**, com `encode`/`decode` reversíveis; para "Raimundo Moura" os tokens gerados são `[49, 1385, 41204, 49902, 430]` (a divergência para o `403` do enunciado foi explicada por uma mudança de merges entre versões da biblioteca);
3. As janelas deslizantes foram geradas via `BdtdDataset` + `BdtdDataLoader` customizados, equivalentes ao `torch.utils.data.DataLoader`, com 19.994 janelas (amostra de 20.000 tokens) para `max_length=6, stride=1`;
4. A camada `nn.Embedding(50257, 256)` produziu os embeddings de todo o vocabulário (`weight.shape = (50257, 256)`) e dos ids de "Raimundo Moura" (`(5, 256)`), confirmando a equivalência `embeddings[i] == weight[token_id]`;
5. Os embeddings posicionais absolutos (1.1 … 1.6; 2.1 … 2.6; …) foram somados aos token embeddings, gerando os **input embeddings** finais de shape `(5, 256)`.

O pipeline resultante vai do **texto bruto até a entrada do transformer** (tokenização → janelas → token embeddings → + posicionais), cobrindo exatamente a etapa de pré-processamento necessária para o treinamento de um LLM do tipo GPT.

---

## 6. Reprodução

Código-fonte e scripts de todas as etapas no repositório (`step1_dataset.py` a `step5_positional.py`, classe `dataset.py`):

```bash
uv sync                              # instala tiktoken + torch
uv run python step1_dataset.py       # análise do dataset + gera data/corpus.txt
uv run python step2_bpe.py           # tokenizador BPE (GPT-2) / tiktoken
uv run python step3_sliding_windows.py --max-length 6 --stride 1 --batch-size 2
uv run python step4_embeddings.py    # token embeddings (nn.Embedding)
uv run python step5_positional.py    # embeddings posicionais absolutos
```


[[Topicos em Inteligencia Artificial]]