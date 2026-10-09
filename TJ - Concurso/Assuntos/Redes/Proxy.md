
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

O Forward Proxy ( Proxy Direto ) eh a modalidade de proxy 

---

[[Assuntos]]
[[Questao 18 - 2024]]