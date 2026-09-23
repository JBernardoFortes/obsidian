
---

O **SSL** ( Secure Sockets Layer ) e o **TLS** ( Transport Layer Security ) sao os dois protocolos de criptografia responsaveis por garantir a seguranca, integridade e privacidade nas comunicacoes via internet. Embora frequentemente tratados como sinonimos no mercado, eles representam duas geracoes tecnologicas distintas

---

### 1. SSL ( Secure Sockets Layer )

Criado na decada de 1990 pela Netscape, o SSL foi o primeiro protocolo amplamente adotado para permitir transacoes e comunicacoes seguras na internet.

Atualmente todas as versoes estao **Formalmente obsoletas e descontinuadas** devido a graves vulnerabilidades de seguranca descobertas ao longo dos anos

### 2. TSL ( Transport Layer Security )

Criado em 1999 pelo IETF como o sucessor padronizado e aprimorado do SSL 3.0

O TLS eh o padrao ativo e obrigatorio no setor.

	Comercialmente, o termo "SSL" continua a ser amplamente utilizado por fornecedores e autoridades certificadoras (como ao vender um "Certificado SSL"), mas o protocolo executado no fundo eh estritamente o TLS.

---

### 3. Diferencas tecnicas principais

Embora ambos compartilhem o objetivo de criar canais criptografados, o TLS introduziu mudancas profundas na arquitetura e no funcionamento:

1. **Processo de Handshake**: 
	1. **SSL**: Realiza uma conexao explicita e lenta, exigindo mais etapas ( Round-trips ) de troca de pacotes entre o cliente e o servidor
	2. **TLS**: Executa uma conexao implicita e mais rapida, reduzindo o numero de etapas e pacotes ne
2. **Autenticacao e integridade de Mensagens**:
	1. **SSL**: Utilizava **MAC**( Message Authentication Code) baseado em algoritmos de hash antigos como o **MD5**, vulneraveis a ataque de colisao
	2. **TLS**: Adotou o **HMAC**( Hash-based Message Authentication Code ), um mecanismo mais seguro e resistente a adulteracoes.
3. **Mensagens de Alerta (Alert Messages)**:
	1. **SSL**: Possuia apenas dois tipos de mensagens de erro ( Aviso e Fatal ), transmitidas em **texto claro (sem criptografia)**
	2. **TLS**: Criptografa todas as mensagens de alerta e introduziu notificacoes especificas , como o alerta de encerramento seguro de sessao ( close_notify )
4. **Pacotes de Criptografia ( Cipher Suites )**:
	1. **SSL**: Mantinha suporte a algoritmos antigos e inseguros
	2. **TLS**: Removeu cifras obsoletas (como RC4 e MD5) e passou a exigir algoritmos de criptografia moderna com **Sigilo Perfeito para Apoiadores** (Forward Secrecy), garantindo que, mesmo que uma chave privada seja vazada no futuro, as sessoes passadas nao possam ser decifradas.

---

### 4. Funcionamento Pratico : A Criptografia Hibrida

O SSL/TLS atua na camada intermediaria entre a **Aplicacao** ( como o HTTP ) e o **Transporte** (TCP). Para conciliar alta seguranca e alto desempenho, a conexao utiliza **criptografia hibrida**:


```text
┌──────────────────────┐                         ┌──────────────────────┐
│  Cliente / Navegador │                         │    Servidor Web      │
└──────────┬───────────┘                         └──────────┬───────────┘
           │                                                │
           │  (1) Criptografia Assimétrica                  │
           │        → Handshake                             │
           │───────────────────────────────────────────────>│
           │                                                │
           │  • Autenticação via Certificado                │
           │  • Negociação da Chave de Sessão               │
           │                                                │
           │  (2) Criptografia Simétrica                    │
           │        → Transmissão de Dados                   │
           │<══════════════════════════════════════════════>│
           │                                                │
           │  • Chave de sessão utilizada                  │
           │  • Transmissão rápida e eficiente              │
           │                                                │
```

- **Fase Assimetrica ( Troca de Chaves )**: O servidor envia seu **Certificado Digital** ( que contem sua chave publica e eh emitido por uma Autoridade Certificadora - CA ). O navegador verifica a autenticidade do certificado. Em seguida, ambos usam a chave publica/privada para negociar de forma segura uma **chave simetrica temporaria** (chave de sessao).
- **Fase Simetrica ( Trafego de Dados )**: Com a chave de sessao estabelecida, a comunicacao passa a utilizar a **c**

---

[[Protocolo HTTPS]]
[[Criptografia simetrica e assimetrica]]