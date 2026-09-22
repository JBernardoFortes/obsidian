[[Assuntos]]


A tecnologia TRIM representa um dos comandos de integracao mais fundamentais entre o sistema operacional e os dispositivos de armazenamento de estado solido (Solid-State Drives - SSDs). sua criacao foi indispensavel para contornar as limitacoes fisicas das memorias Flash NAND e evitar a degradacao drastica de desempenho e da vida util dessas unidades ao longo do tempo

----

### 1. A Arquitetura da memoria Flash NAND e a Assimetria Fisico-Logica

Para compreender a necessidade do TRIM, eh essencial entender o comportamento fisico das memorias Flash NAND. Ao contrario das memorias DRAM volateis, a NAND retem informacoes sem necessidade de energia eletrica ao aprisionar cargas eletricas em transistores de portas flutuantes ( Floating Gate ) ou charge trap por meio de tunelamento eletrico.

Entretanto, as memorias Flash possuem uma limitacao arquitetural conhecida como assimetria de leitura/escrita e apagamento:

- **Paginas** : As operacoes de apagamento eletrico so podem ser executadas em grupos maiores chamados blocos, que agrupam dezeznas de centenas de paginas
- **Blocos** : As operacoes de apagamento eletrico so podem ser executadas em grupos maiores chamados blocos, que agrupam dezenas ou centenas de paginas.
- **Impossibilidade de sobrescrita direta** : Uma celula Flash nao consegue sobrescrever um dado existente diretamente. Para regravar informacao em uma pagina ocupada, a celula precisa ser previamente limpa e zerada - o que exige o apagamento previo do bloco inteiro ao qual aquela pagina pertence.