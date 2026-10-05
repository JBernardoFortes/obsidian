
---

## 1. Conceito Fundamental de Redes Virtuais Privadas ( VPN )

### 1.1 Definicao e Mecanismo de Tunelamento Virtual

Uma Rede Virtual Privada ( VPN - Virtual Private Network ) eh uma tecnologia desenvolvida para estabelecer canais de comunicacao virtuais e criptografadas ("tuneis") sobre infraestruturas de redes publicas e nao confiaveis, como a internet. O candidato deve atentar para o fato de que a VPN nao cria um meio fisico novo, mas sim uma sobreposicao logica ( overlay ) segura sobre uma rede subjacente ( underlay ).

- **Reducao de Custos e Eliminacao de Enlaces Dedicados**: A VPN elimina a necessidade de contratacao de circuitos fisicos dedicados ou linhas privadas alugadas ( conexoes ponto a ponto / WANs dedicadas ), permitindo a transmissao segura de dados corporativos com reducacao drastica de custos operacionais.
- **Mecanismo de Encapsulamento**: A comunicacao ocorre via tunelamento, processo no qual os pacotes de dados originais ( carga util ou payload ) sao envelopados dentro de novos pacotes criptografados antes de trafegares pela rede publica. Dessa forma, caso os dados sejam interceptados por terceiros durante o trajeto, permanecerao totalmente ilegiveis.

### 1.2 Os Quatro Pilares de Seguranca da VPN

Nas provas de concursos publicos ( especialmente Cebraspe, FGV e FCC ), a cobranca sobre as garantias da informacao em uma VPN fundamenta-se estritamente em quatro pilares essenciais:

1. **Confidencialidade**: Garantida pelo uso de algoritmos de criptografia simetria e assimetrica ( como AES, 3DES ou RSA ), transformando o texto em claro (plaintext) em um texto cifrado (ciphertext) indecifravel sem a devida chave criptografica
2. **Integridade**: Garantia de que a mensagem nao foi alterada, adulterada ou corrompida durante o transito na rede publica. Eh assegurada mediante a aplicacao de funcoes de hash criptografico de via unica, como o **SHA-256**.
3. **Autenticidade**: Confirmacao rigorosa e inequivoca da identidade das partes envolvidas na comunicacao ( Emissor e receptor ) ou do proprio servidor de VPN antes do estabelecimento da sessao
4. **Privacidade / Anonimato Relativo**: Ocultamento dos enderecos IP originais e do conteudo das aplicacoes em relacao a intermediarios e provedores situados na rede publica

---

## 2. O Protocolo IPsec ( Camada 3 / Rede )

### 2.1 VIsao Geral da Arquitetura IPsec

O **IPsec ( Internet Protocol Security )** eh uma suite flexivel de protocolos de seguranca que atua estritamente na **Camada 3 (Rede)** do modelo OSI / TCP-IP. Como opera na camada de rede, o IPsec oferece uma protecao transparente para todas as aplicacoes e protocolos das camadas superiores ( como HTTP, FPT e SMTP ), sem exigit adaptacoes nos softwares de usuario final.

### 2.2 Modos de Operacao: Tunel vs. Transporte

As bancas de concurso exploram exaustivamente a diferenca estrutural entre os dois modos de operacao do IPsec:

- **Modo Transparente**: Criptografia **apenas a carga util(payload)** do pacote IP original, mantendo o cabecalho IP original visivel e inalterado. Eh o modo indicado para comuincacoes diretas de host a host ( host-to-host ), onde ambos os computadores suportam o IPsec nativamente
- **Modo Tunel**: Criptografa **todo o pacote IP original** (Cabecalho IP original + payload) e insere um **novo cabecalho IP externo** para roteamento entre os gateways. Eh a modalidade padrao e obrigatoria para conexoes gateway a gateway (site-to-site) e cliente a gateway (remote acess)

---

[[Assuntos]]
[[Questao 17 - 2024]]
