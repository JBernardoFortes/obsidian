[[TSE]]

Dicionario de dados feito a partir do estudo das APIs e dos dados fornecidos

## TSE - Dados de eleicoes

#### Candidatos 
##### Tabela:

# Dicionário de Dados - Tabela CONSULTA_CAND (TSE)

Este dicionário descreve a estrutura dos dados contidos na tabela de consulta de candidaturas (`CONSULTA_CAND_<ANO>_<UF>`), conforme a documentação oficial do Tribunal Superior Eleitoral (TSE).


## 1. Considerações e Regras Gerais

* **Codificação de Caracteres:** `Latin 1` (ISO-8859-1).
* **Delimitador de Campos:** Ponto e vírgula (`;`).
* **Qualificador de Texto:** Aspas ( `" "` ) em todos os campos (inclusive numéricos).
* **Valores Especiais / Ausentes:**
  * `#NULO` (texto) ou `-1` (numérico): Informação em branco no banco de dados.
  * `#NE` (texto) ou `-3` (numérico): Não existente / Não registrado naquele ano eleitoral.
* **Dados Pessoais Protegidos / Não Divulgáveis (LGPD / Res. TSE nº 23.729/2024):**
  * Para o campo **NR_CPF_CANDIDATO** e outros dados protegidos:
    * Campos numéricos: `-4` (exceto idade).
    * Campos de texto: `"NÃO DIVULGÁVEL"`.
    * Datas e idade: `""` (vazio).
* **Valores Especiais para UF (Sigla do Estado):**
  * `BR`: Âmbito nacional.
  * `VT`: Voto em trânsito.
  * `ZZ`: Exterior.


## 2. Dicionário dos Campos

### 2.1. Controle e Identificação da Extração

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DT_GERACAO** | Data | Data da extração dos dados para geração do arquivo. | DD/MM/AAAA |
| **HH_GERACAO** | Hora | Hora da extração dos dados (Horário de Brasília). | HH:MM:SS |
| **ANO_ELEICAO** | Numérico | Ano de referência da eleição ordinária correspondente. | AAAA |


### 2.2. Dados da Eleição

| Variável            | Tipo     | Descrição                                               | Domínio / Valores Possíveis                                                 |
| :------------------ | :------- | :------------------------------------------------------ | :-------------------------------------------------------------------------- |
| **CD_TIPO_ELEICAO** | Numérico | Código do tipo de eleição.                              | `1`: Eleição Suplementar<br>`2`: Eleição Ordinária<br>`3`: Consulta Popular |
| **NM_TIPO_ELEICAO** | Texto    | Nome/Descrição do tipo de eleição.                      | Ex: `ELEIÇÃO ORDINÁRIA`, `ELEIÇÃO SUPLEMENTAR`, `CONSULTA POPULAR`          |
| **NR_TURNO**        | Numérico | Número do turno da eleição.                             | `1`, `2`                                                                    |
| **CD_ELEICAO**      | Numérico | Código único da eleição por turno na Justiça Eleitoral. | Ex: `619`                                                                   |
| **DS_ELEICAO**      | Texto    | Descrição da eleição.                                   | Ex: `Eleições Municipais 2024`                                              |
| **DT_ELEICAO**      | Data     | Data da realização da eleição.                          | DD/MM/AAAA                                                                  |
| **TP_ABRANGENCIA**  | Texto    | Âmbito territorial e administrativo do pleito.          | `M`: Municipal<br>`E`: Estadual<br>`F`: Federal                             |


### 2.3. Localidade e Cargo

| Variável     | Tipo     | Descrição                                               | Domínio / Valores Possíveis                                              |
| :----------- | :------- | :------------------------------------------------------ | :----------------------------------------------------------------------- |
| **SG_UF**    | Texto    | Sigla da Unidade da Federação de candidatura.           | Siglas das UFs, `BR`, `VT` ou `ZZ`                                       |
| **SG_UE**    | Texto    | Sigla da Unidade Eleitoral (Código do Município ou UF). | Ex: `BR`, Sigla da UF, ou Código TSE do Município                        |
| **NM_UE**    | Texto    | Nome da Unidade Eleitoral.                              | Ex: `"Brasil"`, Nome do Estado ou Nome do Município                      |
| **CD_CARGO** | Numérico | Código do cargo disputado.                              | Ex: `1` (Presidente), `3` (Governador), `11` (Prefeito), `13` (Vereador) |
| **DS_CARGO** | Texto    | Descrição do cargo.                                     | Ex: `PREFEITO`, `VICE-PREFEITO`, `VEREADOR`, `GOVERNADOR`, etc.          |


### 2.4. Identificação do Candidato

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SQ_CANDIDATO** | Numérico | Sequencial único do candidato na eleição (gerado pelo TSE). | Código sequencial numérico interno |
| **NR_CANDIDATO** | Numérico | Número do candidato na urna eletrônica. | Número de votação |
| **NM_CANDIDATO** | Texto | Nome completo do candidato. | Texto |
| **NM_URNA_CANDIDATO** | Texto | Nome do candidato exibido na urna. | Texto |
| **NM_SOCIAL_CANDIDATO** | Texto | Nome social de travestis ou transexuais (Decreto 8.727/16). | Texto ou `#NULO` |
| **NR_CPF_CANDIDATO** | Numérico | CPF do candidato (Protegido por sigilo desde 2024). | `-4` (quando não divulgável) ou CPF |
| **DS_EMAIL** | Texto | E-mail do candidato. | `"NÃO DIVULGÁVEL"` ou Endereço de e-mail |
| **CD_SITUACAO_CANDIDATURA**| Numérico | Código da situação do registro (Aplicável até 2022). | Código numérico |
| **DS_SITUACAO_CANDIDATURA**| Texto | Descrição da situação do registro (Aplicável até 2022). | Texto |


### 2.5. Agremiação, Partido e Coligação

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **TP_AGREMIACAO** | Texto | Forma como o candidato concorre na eleição. | `Partido Isolado`<br>`Coligação`<br>`Federação` |
| **NR_PARTIDO** | Numérico | Número do partido político. | Número do partido |
| **SG_PARTIDO** | Texto | Sigla do partido do candidato. | Ex: `PL`, `PT`, `UNIÃO`, `MDB` |
| **NM_PARTIDO** | Texto | Nome oficial do partido do candidato. | Texto |
| **NR_FEDERACAO** | Numérico | Número da federação partidária. | Código da federação ou `-1` |
| **NM_FEDERACAO** | Texto | Nome da federação partidária. | Texto ou `#NULO` |
| **SG_FEDERACAO** | Texto | Sigla da federação partidária. | Texto ou `#NULO` |
| **DS_COMPOSICAO_FEDERACAO** | Texto | Lista das siglas dos partidos que compõem a federação. | Ex: `PT/PC do B/PV` ou `#NULO` |
| **SQ_COLIGACAO** | Numérico | Sequencial único da coligação no TSE. | Código numérico ou `-1` |
| **NM_COLIGACAO** | Texto | Nome oficial da coligação. | Texto |
| **DS_COMPOSICAO_COLIGACAO**| Texto | Siglas dos partidos que formam a coligação ou federação. | Siglas separadas por `,` (coligação) ou `/` (federação) |


### 2.6. Dados Perfil Demográfico e Socioeconômico

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SG_UF_NASCIMENTO** | Texto | UF de nascimento do candidato. | Sigla do estado ou `#NULO` |
| **DT_NASCIMENTO** | Data | Data de nascimento do candidato. | DD/MM/AAAA ou `""` |
| **NR_TITULO_ELEITORAL_CANDIDATO** | Numérico | Número do Título de Eleitor. | Número do título ou `-4` |
| **CD_GENERO** | Numérico | Código do gênero do candidato. | `2`: Masculino<br>`4`: Feminino |
| **DS_GENERO** | Texto | Descrição do gênero. | `MASCULINO`, `FEMININO` |
| **CD_GRAU_INSTRUCAO** | Numérico | Código do grau de escolaridade. | `1`: Analfabeto<br>`2`: Lê e escreve<br>`3`: Ensino fundamental incompleto<br>`4`: Ensino fundamental completo<br>`5`: Ensino médio incompleto<br>`6`: Ensino médio completo<br>`7`: Superior incompleto<br>`8`: Superior completo |
| **DS_GRAU_INSTRUCAO** | Texto | Descrição do grau de instrução. | Texto correspondente ao código |
| **CD_ESTADO_CIVIL** | Numérico | Código do estado civil. | `1`: Solteiro(a)<br>`3`: Casado(a)<br>`5`: Viúvo(a)<br>`7`: Separado(a) judicialmente<br>`9`: Divorciado(a) |
| **DS_ESTADO_CIVIL** | Texto | Descrição do estado civil. | Texto correspondente ao código |
| **CD_COR_RACA** | Numérico | Código da cor/raça (padrão IBGE). | `01`: Branca<br>`02`: Preta<br>`03`: Parda<br>`04`: Amarela<br>`05`: Indígena<br>`06`: Não Informado |
| **DS_COR_RACA** | Texto | Descrição da autodeclaração de cor ou raça. | Texto correspondente ao código |
| **CD_OCUPACAO** | Numérico | Código da ocupação principal do candidato. | Código numérico da CBO |
| **DS_OCUPACAO** | Texto | Descrição da ocupação principal. | Ex: `ADVOGADO`, `EMPRESÁRIO`, `DEPUTADO`, etc. |


### 2.7. Resultado da Eleição

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_SIT_TOT_TURNO** | Numérico | Código da situação de totalização no turno. | Código numérico do status |
| **DS_SIT_TOT_TURNO** | Texto | Status final do candidato no turno. | Ex: `ELEITO`, `NÃO ELEITO`, `ELEITO POR QP`, `SUPLENTE`, `2º TURNO` |
