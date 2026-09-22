
A "clonagem" ou replicacao de hardware em um processador superescalar nao eh um processo dinamico de software, mas sim uma duplicacao fisica de circuitos integrados gravados no proprio chip de silicio durante a sua fabricacao.

Para que essa estrutura duplicada funcione sem gargalos de comunicacao, os projetistas de microarquitetura constroem uma infraestrutura especial no chip.

--- 

## 1. Duplicacao Fisica de Unidades Funcionais

Em vez de projetar apenas um circuito calculador, os engenheiros esculpem multiplos blocos logicos identicos ou especializados lado a lado no silicio.

- **Multiplas ALUs (Unidades logicas e aritmeticas)**: Varios circuitos capazes de somar, subtrair e fazer operacoes logicas inteiras simultaneamente.
- **Multiplas FPUs (Unidades de ponto flutuante)**: Circuitos dedicados a operacoes matematicas de alta precisao e numeros decimais
- **Multiplas LSUs (Unidades de Load/Store)**: Modulos pararelos responsaveis por ler e escrever dados na memoria cache e RAM.


--- 

## 2. Amplicacao dos Caminhos de Dados ( Datapath )

Ter varias "Calculadoras" internas nao traz ganho se os dados nao chegarem ate elas ao mesmo tempo. Por isso, a arquitetura expande as vias de comunicacao internas.

- **Busca e decodificacao larga ( Wide Fetch/ Decode)**: Os barramentos de instrucao sao alargados para buscar e decodificar blocos contendo 2,4 ou mais instrucoes da memoria de uma so vez a cada ciclo de clock ( lendo pacotes de 64 ou 128 Bits )
- **Banco de registradores multi-portas ( Multi-Ported register file )**: Para permitir que varias unidades funcionais leiam e escrevam registradores no mesmo instante sem colidirem, o banco de registradores ganha multiplas portas fisicas de leitura e escrita trabalhnado em paralelo

--- 

## 3. Circuitos de Controle e Distribuicao

Para gerenciar qual das unidades clonadas vai executar cada instrucao, sao adicoinados circuitos de suporte:

- **Estacoes de Reserva ( E)

---

