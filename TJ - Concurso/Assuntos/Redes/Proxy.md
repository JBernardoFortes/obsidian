
---

### 1. Conceito e Funcionamento de Servidores Proxy

Um servidor proxy eh um no ou servidor intermediario posicionado em uma rede de computadores que atua no fluxo de comunicacao entre os clientes ( usuarios da rede interna ) e os recursos externos ou servidores de destino. Sua funcao primaria eh intermediar a troca de trafego de dados, gerenciando cada requisicao enviada e a respectiva resposta retornada

#### 1.1 O Papel do Intermediario de Redes

A intermediacao de requisicoes ocorre quando o servidor proxy se estabelece fisica ou logicamente entre as duas pontas da comunicacao. Em vez de o cliente estabelecer uma conexao direta e nao filtrada com o servidor final na internet, a solicitacao eh encaminhada ao proxy, que a recebe, inspeciona, aplica regra de controle, processa e a repassa ao destino. O trafego de retorno percorre o caminho inverso, sendo entregue ao cliente somente apos a validacao do intermediario

- **Intermediacao de requisicoes**: Recebe as solicitacoes dos clientes e as gerencia antes de repassa-las a rede externa ou ao servidor final
- **Controle e filtragem de trafego**: Posiciona-se estrategicamente no fluxo de comunicacao entre as pontas para aplicar regras de acesso, politicas de seguranca e monitoramento
- **Isolamento de pontas**: Evita a conexao direta entre a origem ( cliente ) e o destino final ( servidor ), impedindo a exposicao da topologia interna da rede.

#### 1.2 Recursos e Finalidades Basicas

O emprego de servidores intermediarios na arquitetura de redes atende a objetivos estrategicos e operacionais bem definidos: 

- **Gerenciamento de acesso e controle**: Aplica politicas institucionais de restricao, bloqueio ou liberacao de conteudos e servicos com base em URLs, dominios ou categorias.
- **Anonimato e mascaramento**: Oculta os identificadores da origem do trafego ( como o endereco IP privado do cliente ) ao intermediar a comunicacao com a rede externa.
- **Otimizacao por meio de cache**: Armazena localmente em memoria ou disco as respostas de requisicoes frequentes para entrega-las com menor latencia em acessos futuros, reduzindo o consumo de largura de banda do link de internet.

### 2. Forward Proxy ( Proxy Direto )

O Forward Proxy ( Proxy Direto ) eh a modalidade de proxy voltada para a protecao, controle e atendimento as demands dos clientes e usuarios de uma rede interna corporativa ou institucional.

#### 2.1 Localizacao e Atuacao na Redes de Clientes

O Forward Proxy fica posicionado no perimetro de saida da rede local ( LAN ) em direcao a internet publica. Ele monitora e processa o trafego de saida ( Outbound traffic ), garantindo que todas as solicitacoes de navegacao e acesso a servicos externos geradas pelas estacoes de trabalho internas passem obrigatoriamente pela sua estrutura de filtragem.

#### 2.2 Funcionalidades de Controle e Auditoria

A implementacao do Forward Proxy prove ferramentas essenciais para a gestao da rede de clientes:

- **Gestao de Acesso e Seguranca do Cliente**:
	- **Controle e filtragem de conteudo**: Bloqueio ativo de sites, portas, protocolos e categorias de enderecos web nao autorizados pelas politicas de seguranca da informacao
	- **Auditoria e monitoramento de navegacao**: Geracao de registros detalhados ( logs ) do historico de acessos, volume de dados trafegados e horarios de conexao por usuario ou endereco IP interno.
	- **Mascaramento de IP do cliente**: Substituicao do endereco IP interno do usuario pelo endereco IP do proprio proxy frente aos servidores de destino na internet
	- **Armazenamento em cache local**: Retencao temporaria de conteudos web e arquivos estaticos recorrentes para acelerar o tempo de resposta e poupar link de dados da organizacao.

### 3. Reverse Proxy ( Proxy Reverso )

Diferente da modalidade direta, o Reverse Proxy ( Proxy Reverso ) eh direcionado para a infraestrutura de servidores, atuando no recebimento e gerenciamento do trafego vindo da internet em direcao aos servicos internos

#### 3.1 Posicionamento e Arquitetura do Proxy Reverso

O Proxy Reverso fica posicionado na entrada da infraestrutura do servidor, frequentemente alocado na Zona Desmilitarizada ( DMZ ) da rede. Ele funciona como uma interface intermediaria obrigatoria entre os clientes externos ( usuarios na internet ) e os servidores web ( web servers ) ou servidores de aplicacao internos. No trafego de entrada ( inbound traffic ), o cliente externo conecta-se ao Proxy Reverso pensando estar conectando diretamente ao servidor final

#### 3.2 Gerenciamento de Requisicoes e Balanceamento de Carga ( Load Balancing ) 

Ao receber as requisicoes externas, o Proxy Reverso analisa o trafego e as distribui de forma otimizada entre os multiplos servidores web da infraestrutura interna. Essa funcionalidade eh a base do **balanceamento de carga ( load balancing )**, que distribui uniformemente a carga de trabalho, previne a sobrecarga de servidores individuais, melhora o tempo de resposta e garante a alta disponibilidade ( High Availability ) do sistema mesmo em picos de acesso.

#### 3.2 Desempenho e Protecao Adicional contra Ataques Diretos

Alem de otimizar o desempenho do sistema por meio de recursos como aceleracao por cache, compressao de dados e terminacao SSL/TLS, o Proxy Reverso oculta completamente a arquitetura interna e os enderecos IP reais dos servidores de aplicacao
	**Protecao dos servidores Centrais**: Ao posicionar o Proxy Reverso como porta de entrada unica para as requisicoes externas, a topologia e os enderecos IP reais dos servidores web centrais permanecem ocultos da internet publica, estabelecendo uma camada defensiva essencial que impede e previne ataques diretos contra a infraestrutura central.


## Ilustracao de Forward Proxy vs. Reverse Proxy:

![[0196-forward-proxy-vs-reverse-proxy.png]]


### 4. Comparativo Pratico: Forward Proxy vs. Reverse Proxy


| Criterio de Comparacao      | Forward Proxy                                                                                | Reverse Proxy                                                                                                            |
| --------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Localizacao na rede         | Na saida da rede local /<br>interna                                                          | Na entrada da infraestrutura de servidores                                                                               |
| A quem protege / representa | Protege e representa os **Clientes / Usuarios** da rede interna                              | Protege e representa o **servidor / infraestrutura** de aplicacao                                                        |
| Principal Objetivo          | Controle de navegacao, Auditoria do usuario e economia de banda via cache local              | Balanceamento de carga, alta disponibilidade, desempenho e ocultacao de servidores                                       |
| Tipo de Trafego gerenciado  | Trafego de saida ( Outbound ): Das estacoes internas para a internet                         | Trafego de entrada ( inbound ): Dos cliientes externos da internet para os servidores interos                            |
| Exemplos associados         | Filtro de conteudo empresarial, bloqueio de redes sociais e logs de navegacao do funcionario | Distribuicao de carga em portais corporativos, terminacao SSL / TLS e protecao contra varreduras de IP na infraestrutura |
### 5. Diferenciacao de Tecnologias Correlatas de Rede e Seguranca

Para obter alto rendimento em provas teoricas de concursos publicos, eh indispensavel diferenciar a intermediacao executada por Proxies das demais solucoes de infraestrutura e perimetro de seguranca

#### 5.1 Proxy vs Firewall, NAT e VPN

1. **Proxy ( Intermediario de Aplicacao )**: Solucao que atua nas camadas superiores do modelo OSI ( Camada de Aplicacao - Camada 7 ), intermediando solicitacoes de servicos especificos ( como HTTP e HTTPS ). ela nao se limita a liberar ou bloquear portas, mas inspeciona, altera ou responde as requisocoes em nome das pontas ( seja controlando usuarios no Forward ou balanceando servidores no Reverse ).
2. **Firewall ( Filtro de Trafego e Inspecao de Seguranca )**: Dispositivo ou software focado no controle de acesso ao perimetro da rede. Inspeciona pacotes de dados e conexoes com base em tabelas de regras ( enderecos IP de origem / destino, portas e protocolos ) e estado da conexao ( stateful inspection ). Diferente do proxy, o firewall tipicamente atua nas camadas de Rede e Transporte ( Camadas 3 e 4 ) e eh posicionado nas fronteiras de rede ( como entre a internet, a DMZ e a Rede Interna ) para permitir ou bloquear o trafego.
3. **NAT ( Netword Address Translation - Traducao de enderecos de rede )**: Mecanismo de rede configurado em roteadores ou firewalls para reescrever os cabecalhos IP dos pacotes. Permite que multiplos computadores de uma rede interna operando com enderecos IP privados nao roteaveis compartilhem um unico endereco IP publico para acessar a internet, sem realizar qualquer tipo de intermediacao ou filtragem na camada de aplicacao.
4. **VPN ( Virtual Private Network - Rede Privada Virtual )**: Tecnologia criada para estabelecer um tunel de comunicacao seguro e criptografado sobre uma rede publica nao confiavel ( como a internet ). Garante confidencialidade, integridade e autenticidade para o trafego de dados entre matriz e filiais ou entre usuarios remotos e rede corporativa.

#### 5.2 Camadas de Protecao e Criptografia Associadas ( HTTP vs. HTTPS, FTP e SSL / TLS )

A atuacao dos servidores intermediarios conecta-se diretamente aos protocolos de transferencia de dados da web e as camadas de seguranca criptografica:

- **HTTP ( HyperText Transfer Protocol ) vs. FTP ( File Transfer Protocol )**: O HTTP eh o protocolo fundamental da web projetado para a transferencia e exibicao de paginas ( hipertexto ), combinando textos, imagens e elementos estaticos renderizados diretamente pelo navegador. O FTP, por sua vez, eh um protooclo dedicado especificamente a transferencia bruta de arquivos ( upload e download ) entr

---

[[Assuntos]]
[[Questao 18 - 2024]]