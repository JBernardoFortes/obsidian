
---
### 1. Introducao aos Protocolos de Navegacao: HTTP vs. HTTPS

A navegacao na World Wide Web baseia-se em protocolos que definem como as informacoes sao trocadas entre o seu navegador e o servidor.

- **HTTP ( HyperText Transfer Protocol )**: Eh o protocolo fundamental de transferencia de hipertexto. Ele define como as requisicoes e respostas de paginas, imagens e recursos sao realizadas
- **HTTPS ( HyperText Transfer Protocol Secure )**: Eh a versao segura do HTTP. Ele adiciona uma camada de protecao criptografica ( via SSL ou TLS ) a comunicacao.

#### **Principal Diferenca Tecnica**

Enquanto o HTTP transmite dados em texto claro (passiveis de interceptacao em redes Wi-Fi compartilhadas ), o HTTPS cifra o conteudo, garantindo a privacidade e protegendo contra a leitura por terceiros

---

### 2. O Papel do SSL/TLS e a Criptografia Hibrida

A seguranca do HTTPS nao eh nativa do protocolo, mas fornecida por camadas adicionais. O protocolo SSL ( Secure Sockets Layer ) foi o precursor, sendo sucedido pelo TLS (Transport Layer Security ), que eh a versao morderna e evoluida utilizada atualmente.

**Contexto Historico e Viabilidade**

Antigamente, o HTTPS era reservado apenas a bancos e e-commerces devido ao **alto custo computacional** e a limitacao do poder de processamento da epoca. Hoje, com a evolucao dos processadores, o HTTPS tornou-se o padrao global, sendo inclusive um criterio de indexacao favorecido por mecanismos de busca ( Como o Google ) para incentivar a seguranca geral da rede.

O funcionamento do HTTPS baseia-se em uma **Criptografia Hibrida**, dividida em duas fases claras:

1. **Handshake ( Negociacao Inicial Segura )**: Nesta fase, utiliza-se a **criptografia assimetrica** (chaves publicas e privadas). O objetivo eh a autenticacao do servdor e a troca de chaves de seguranca de forma protegida
2. **Trafego de Dados**: Uma vez estabelecida a conexao, passa-se a utilizar a **crip**

---

[[Assuntos]]
[[Questao 27 - 2025]]
