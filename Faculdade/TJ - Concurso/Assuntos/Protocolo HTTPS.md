
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
2. **Trafego de Dados**: Uma vez estabelecida a conexao, passa-se a utilizar a **criptografia simetrica** para a transmissao das infomacoes.

**Dicas de Prova**: A criptografia simetrica eh preferida para o trafego continuo de dados por ser tecnicamente mais rapida e eficinte para grandes volumes de informacao, enquanto a assimetrica eh usada paenas no inicio ( handshake ) pela sua seguranca na troca de chaves

---

### 3. Certificados Digitais e Autoridades Certificadoras ( CA )

O Certificado SSL/TLS eh o documento digital que viabiliza a conexao segura.

- **Finalidade**: Estabelecer a conexao criptografada e atestar a identidade do titular do dominio
- **Emissao**: Eh emitido por uma Autoridade Certificadora (CA) confiavel, que verifica e atesta quem eh o administrador do site antes de fornecer o documento.

	O Certificado SSL/TLS contem a **chave publica do servidor**, elemento indispensavel para o processo de handshake e para garantir que o navegador esta se comunicando com o servidor correto

---

### 4. Diferenciacao Adicional: HTTP vs FTP

Eh comum as bancas compararem esses dois protocolos para confundir o candidato:

- **HTTP/HTTPS**: Projetado para a exibicao de paginas web(hipertexto), combinando textos e imagens que sao renderizados visualmente pelo navegador.
- **FTP (File Transfer Protocol)**: Projetado especificamente para a **transferencia bruta de arquivos** entre sistemas, sem qualquer preocupacao com a renderizacao visual ou exibicao de paginas

--- 

### 5. Tabela comparativa


| Criterio          | HTTP                  | HTTPS                   |
| ----------------- | --------------------- | ----------------------- |
| Criptografia      | Nenhuma (Texto claro) | Sim ( SSL ou TLS )      |
| Porta Padrao      | 80                    | 443                     |
| Seguranca         | Baixa                 | Alta                    |
| Tipo de Dados     | Texto Claro           | Cifrado / Criptografado |
| Protocolo de Base | Nenhum                | SSL/TLS                 |


---

[[Assuntos]]
[[Questao 27 - 2025]]
