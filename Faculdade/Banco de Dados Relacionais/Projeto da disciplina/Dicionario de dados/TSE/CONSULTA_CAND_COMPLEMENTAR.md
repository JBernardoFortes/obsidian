
Este dicionário descreve a estrutura dos dados contidos na tabela de consulta complementar de candidaturas (`CONSULTA_CAND_COMPLEMENTAR_<ANO>_<UF>`), conforme a documentação oficial do Tribunal Superior Eleitoral (TSE).


## 1. Considerações e Regras Gerais

* **Codificação de Caracteres:** `Latin 1` (ISO-8859-1).
* **Delimitador de Campos:** Ponto e vírgula (`;`).
* **Qualificador de Texto:** Aspas ( `" "` ) em todos os campos (inclusive numéricos).
* **Valores Especiais / Ausentes:**
  * `#NULO` (texto) ou `-1` (numérico): Informação em branco no banco de dados.
  * `#NE` (texto) ou `-3` (numérico): Não existente / Não registrado naquele ano eleitoral.
* **Dados Pessoais Protegidos / Não Divulgáveis (LGPD / Res. TSE nº 23.729/2024):**
  * Para candidatos não divulgáveis, os dados pessoais são preenchidos com:
    * Campos numéricos: `-4` (exceto idade).
    * Campos textuais: `"NÃO DIVULGÁVEL"`.
    * Datas e idade: `""` (vazio).
* **Valores Especiais para UF (Sigla do Estado):**
  * `BR`: Âmbito nacional.
  * `VT`: Voto em trânsito.
  * `ZZ`: Exterior.



## 2. Dicionário dos Campos

### 2.1. Controle e Identificação da Eleição

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DT_GERACAO** | Data | Data da extração dos dados para geração do arquivo. | DD/MM/AAAA |
| **HH_GERACAO** | Hora | Hora da extração dos dados (Horário de Brasília). | HH:MM:SS |
| **ANO_ELEICAO** | Numérico | Ano de referência da eleição ordinária correspondente. | AAAA |
| **CD_ELEICAO** | Numérico | Código único da eleição por turno na Justiça Eleitoral. | Código numérico por turno |
| **SQ_CANDIDATO** | Numérico | Número sequencial do candidato, gerado internamente pelos sistemas eleitorais para a eleição. | Sequencial único do TSE |



### 2.2. Perfil Pessoal, Demográfico e Diversidade

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_NACIONALIDADE** | Numérico | Código da nacionalidade do candidato. | `1`: Brasileira nata<br>`2`: Brasileira (naturalizada)<br>`3`: Portuguesa com igualdade de direitos<br>`4`: Estrangeiro |
| **DS_NACIONALIDADE** | Texto | Descrição da nacionalidade do candidato. | `BRASILEIRA NATA`, `BRASILEIRA (NATURALIZADA)`, etc. |
| **CD_MUNICIPIO_NASCIMENTO** | Numérico | Código de identificação do município de nascimento do candidato. | Código TSE do município |
| **NM_MUNICIPIO_NASCIMENTO** | Texto | Nome do município de nascimento do candidato. | Texto |
| **NR_IDADE_DATA_POSSE** | Numérico | Idade do candidato na data da posse. | Idade calculada com base na data da posse |
| **ST_QUILOMBOLA** | Texto | Indica se o candidato se autodeclara quilombola. | `S`: Sim<br>`N`: Não |
| **CD_ETNIA_INDIGENA** | Numérico | Código da etnia indígena autodeclarada pelo candidato. | Código da etnia no cadastro eleitoral ou `0` |
| **DS_ETNIA_INDIGENA** | Texto | Descrição da etnia indígena autodeclarada pelo candidato. | Nome da etnia ou `NÃO INFORMADA` |



### 2.3. Informações de Campanha e Processuais

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **VR_DESPESA_MAX_CAMPANHA** | Decimal | Valor máximo, em reais, de despesas de campanha declarada pelo partido. | Valor numérico em reais (ex: `15985.08`) |
| **ST_REELEICAO** | Texto | Indica se o candidato concorre à reeleição para o mesmo cargo na mesma circunscrição. | `S`: Sim<br>`N`: Não |
| **ST_DECLARAR_BENS** | Texto | Indica se o candidato declarou possuir bens. | `S`: Sim<br>`N`: Não |
| **NR_PROTOCOLO_CANDIDATURA** | Numérico | Número do protocolo de registro de candidatura. | Código numérico ou `-1` |
| **NR_PROCESSO** | Numérico/Texto | Número do processo de registro de candidatura no PJe. | Número do processo |
| **ST_PREST_CONTAS** | Texto | Indica se o candidato realizou a prestação de contas eleitorais. | `S`: Sim<br>`N`: Não |



### 2.4. Substituição e Suplência

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **ST_SUBSTITUIDO** | Texto | Indica se o candidato foi substituído por outro. | `Sim` / `Não` (ou `S` / `N`) |
| **SQ_SUBSTITUIDO** | Numérico | Número sequencial do candidato que foi substituído pelo candidato corrente. | Sequencial único do TSE ou `-1` |
| **SQ_ORDEM_SUPLENCIA** | Numérico | Ordem da suplência para cargos proporcionais (ou 1º/2º suplente para Senador). | Número de ordem do suplente |
| **DT_ACEITE_CANDIDATURA** | Data/Hora | Data e hora em que foi aceite o registro pela Justiça Eleitoral (para desempate de substituição). | AAAA-MM-DD HH:MM:SS |



### 2.5. Situações Históricas de Julgamento e Urna (Até 2022)

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_DETALHE_SITUACAO_CAND** | Numérico | Código do detalhe da situação do registro (*aplicável até 2022*). | Código numérico ou `-3` (`#NE`) |
| **DS_DETALHE_SITUACAO_CAND** | Texto | Descrição do detalhe da situação do registro (*aplicável até 2022*). | Texto ou `#NE` |
| **CD_SITUACAO_CANDIDATO_PLEITO** | Numérico | Código da situação da candidatura no dia do pleito (*aplicável até 2022*). | Código numérico ou `-3` (`#NE`) |
| **DS_SITUACAO_CANDIDATO_PLEITO** | Texto | Descrição da situação da candidatura no dia do pleito (*aplicável até 2022*). | Texto ou `#NE` |
| **CD_SITUACAO_CANDIDATO_URNA** | Numérico | Código da situação da candidatura na urna (*aplicável até 2022*). | Código numérico ou `-3` (`#NE`) |
| **DS_SITUACAO_CANDIDATO_URNA** | Texto | Descrição da situação da candidatura na urna (*aplicável até 2022*). | Texto ou `#NE` |
| **CD_SITUACAO_CANDIDATO_TOT** | Numérico | Código da situação atual no banco de totalização (*aplicável até 2022*). | Código numérico |
| **DS_SITUACAO_CANDIDATO_TOT** | Texto | Descrição da situação atual no banco de totalização (*aplicável até 2022*). | Ex: `DEFERIDO`, `INDEFERIDO` |



### 2.6. Situações de Urna, Destinação de Votos e Impugnação

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **ST_CANDIDATO_INSERIDO_URNA** | Texto | Indica se o candidato foi inserido na urna eletrônica. | `S`: Sim<br>`N`: Não (ou `SIM`/`NÃO`) |
| **NM_TIPO_DESTINACAO_VOTOS** | Texto | Nome do tipo de destinação dos votos recebidos. | Ex: `Válido`, `Anulado sub judice`, `Anulado` |
| **ST_IMPUGNADO** | Texto | Indica se o candidato teve o registro de candidatura impugnado. | `S`: Sim<br>`N`: Não |



### 2.7. Situações de Julgamento, Cassação e Diplomação (A partir de 2024 / 2018)

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_SITUACAO_JULGAMENTO** | Numérico | Código da situação do registro de candidatura (*a partir de 2024*). | Código numérico |
| **DS_SITUACAO_JULGAMENTO** | Texto | Descrição da situação com relação ao julgamento (*a partir de 2024*). | Ex: `DEFERIDO`, `INDEFERIDO`, `EM JULGAMENTO` |
| **CD_SITUACAO_JULGAMENTO_PLEITO** | Numérico | Código da situação no dia do pleito (*a partir de 2024*). | Código numérico |
| **DS_SITUACAO_JULGAMENTO_PLEITO** | Texto | Descrição da situação no dia do pleito (*a partir de 2024*). | Ex: `DEFERIDO`, `INDEFERIDO` |
| **CD_SITUACAO_JULGAMENTO_URNA** | Numérico | Código da situação na urna (*a partir de 2024*). | Código numérico |
| **DS_SITUACAO_JULGAMENTO_URNA** | Texto | Descrição da situação na urna (*a partir de 2024*). | Ex: `DEFERIDO`, `INDEFERIDO` |
| **CD_SITUACAO_CASSACAO** | Numérico | Código da situação quanto à cassação do mandato (*a partir de 2024*). | Código numérico ou `-1` |
| **DS_SITUACAO_CASSACAO** | Texto | Descrição da situação quanto à cassação do mandato (*a partir de 2024*). | Texto ou `#NULO` |
| **CD_SITUACAO_CASSACAO_MIDIA** | Numérico | Código da situação de cassação no fechamento do sistema/mídia (*a partir de 2024*). | Código numérico ou `-1` |
| **DS_SITUACAO_CASSACAO_MIDIA** | Texto | Descrição da situação de cassação no fechamento do sistema/mídia (*a partir de 2024*). | Texto ou `#NULO` |
| **CD_SITUACAO_DCONST_DIPLOMA** | Numérico | Código da situação no processo de desconstituição do diploma (*a partir de 2024*). | Código numérico ou `-1` |
| **DS_SITUACAO_DCONST_DIPLOMA** | Texto | Descrição da situação no processo de desconstituição do diploma (*a partir de 2024*). | Texto ou `#NULO` |
| **DT_DIPLOMACAO** | Data | Data da diplomação do candidato (*a partir de 2018*). | DD/MM/AAAA ou `#NULO` |
| **CD_SITUACAO_DIPLOMACAO** | Numérico | Código da situação da diplomação (*a partir de 2018*). | Código numérico ou `-1` |
| **DS_SITUACAO_DIPLOMACAO** | Texto | Descrição da situação da diplomação (*a partir de 2018*). | Texto ou `#NULO` |



### 2.8. Dados de Gênero e Cor/Raça Congelados para o FEFC (Fundo Especial de Financiamento de Campanha)

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_GENERO_FEFC** | Numérico | Código do gênero congelado para cálculo da distribuição do FEFC. | `2`: Masculino<br>`4`: Feminino |
| **DS_GENERO_FEFC** | Texto | Descrição do gênero congelado para o FEFC. | `MASCULINO`, `FEMININO` |
| **CD_COR_RACA_FEFC** | Numérico | Código da cor/raça congelado para cálculo da distribuição do FEFC. | `01`: Branca<br>`02`: Preta<br>`03`: Parda<br>`04`: Amarela<br>`05`: Indígena<br>`06`: Não Informado |
| **DS_COR_RACA_FEFC** | Texto | Descrição da cor/raça congelada para o FEFC. | `BRANCA`, `PRETA`, `PARDA`, `AMARELA`, `INDÍGENA`, `NÃO INFORMADO` |