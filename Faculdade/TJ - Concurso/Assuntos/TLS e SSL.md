
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
	1. **SSL**: Realizaca uma conexao explicita e lenta, exigindo mais etapas ( Round-trips ) de troca de pacotes entre o cliente e o servidor
	2. **TLS**: Executa uma conexao implicita e mais rapida, reduzindo o numero de etapas e pacotes necessarios para estabelecer a sessao. O TLS 1.3 otimizou ainda mais esse processo para apenas um tempo de viagem e volta ( 1-RTT )
2. **Autenticacao e integridade de Mensagens**:
	1. **SSL**: Utilizava **MAC**( Message Authentication Code) baseado em algoritmos de hash antigos como o **MD5**, vulneraveis a ataque de colisao
	2. **TLS**: Adotou o **HMAC**( Hash-based )

