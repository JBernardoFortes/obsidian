
[[TSE]]

## 1. Considerações e Regras Gerais

* **Codificação de Caracteres:** `Latin 1` (ISO-8859-1)[cite: 4].
* **Delimitador de Campos:** Ponto e vírgula (`;`)[cite: 4].
* **Qualificador de Texto:** Aspas ( `" "` ) em todos os campos (inclusive numéricos)[cite: 4].
* **Valores Especiais / Ausentes:**
  * `#NULO` (texto) ou `-1` (numérico): Informação em branco no banco de dados[cite: 4].
  * `#NE` (texto) ou `-3` (numérico): Não existente / Não registrado naquele ano eleitoral[cite: 4].
* **Valores Especiais para UF (Sigla do Estado):**
  * `BR`: Âmbito nacional[cite: 4].
  * `VT`: Voto em trânsito[cite: 4].
  * `ZZ`: Exterior[cite: 4].

### Esta tabela contém os dados sobre o **mapeamento das coligações, federações e partidos políticos isolados** que disputaram as **Eleições Municipais** 

## 2. Dicionário dos Campos

### 2.1. Controle e Identificação da Extração

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DT_GERACAO** | Data | Data da extração dos dados para geração do arquivo[cite: 4]. | DD/MM/AAAA |
| **HH_GERACAO** | Hora | Hora da extração dos dados com base no horário de Brasília[cite: 4]. | HH:MM:SS |
| **ANO_ELEICAO** | Numérico | Ano de referência da eleição para geração do arquivo[cite: 4]. | AAAA |



### 2.2. Dados da Eleição

| Variável            | Tipo     | Descrição                                                        | Domínio / Valores Possíveis                                                          |
| :------------------ | :------- | :--------------------------------------------------------------- | :----------------------------------------------------------------------------------- |
| **CD_TIPO_ELEICAO** | Numérico | Código do tipo de eleição[cite: 4].                              | `1`: Eleição Suplementar<br>`2`: Eleição Ordinária<br>`3`: Consulta Popular[cite: 4] |
| **NM_TIPO_ELEICAO** | Texto    | Nome do tipo de eleição[cite: 4].                                | Ex: `ELEIÇÃO ORDINÁRIA`, `ELEIÇÃO SUPLEMENTAR`, `CONSULTA POPULAR`[cite: 4]          |
| **NR_TURNO**        | Numérico | Número do turno da eleição[cite: 4].                             | `1`, `2`[cite: 4]                                                                    |
| **CD_ELEICAO**      | Numérico | Código único da eleição por turno na Justiça Eleitoral[cite: 4]. | Código numérico único[cite: 4]                                                       |
| **DS_ELEICAO**      | Texto    | Descrição da eleição[cite: 4].                                   | Ex: `Eleições Municipais 2024`                                                       |
| **DT_ELEICAO**      | Data     | Data da ocorrência da eleição[cite: 4].                          | DD/MM/AAAA                                                                           |



### 2.3. Localidade e Cargo

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SG_UF** | Texto | Sigla da Unidade da Federação na qual o candidato concorre[cite: 4]. | Siglas das UFs, `BR`, `VT` ou `ZZ`[cite: 4] |
| **SG_UE** | Texto/Numérico | Sigla da Unidade Eleitoral (UF ou Código TSE do Município)[cite: 4]. | Ex: `BR`, Sigla da UF ou Código do Município[cite: 4] |
| **NM_UE** | Texto | Nome da Unidade Eleitoral (Nome do município, da UF ou "Brasil")[cite: 4]. | Ex: `"CAMPO ALEGRE"`, Nome da UF ou `"Brasil"`[cite: 4] |
| **CD_CARGO** | Numérico | Código do cargo ao qual o candidato concorre[cite: 4]. | Ex: `11` (Prefeito), `12` (Vice-prefeito), `13` (Vereador) |
| **DS_CARGO** | Texto | Descrição do cargo ao qual o candidato concorre[cite: 4]. | Ex: `PREFEITO`, `VICE-PREFEITO`, `VEREADOR` |



### 2.4. Dados do Partido, Federação e Coligação

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **TP_AGREMIACAO** | Texto | Forma como o candidato concorre na eleição[cite: 4]. | `Coligação`<br>`Federação`<br>`Partido Isolado`[cite: 4] |
| **NR_PARTIDO** | Numérico | Número oficial do partido político[cite: 4]. | Número do partido (ex: `45`, `13`, `15`) |
| **SG_PARTIDO** | Texto | Sigla do partido político[cite: 4]. | Ex: `PSDB`, `PT`, `MDB`, `PP` |
| **NM_PARTIDO** | Texto | Nome oficial do partido político[cite: 4]. | Texto completo do nome do partido |
| **NR_FEDERACAO** | Numérico | Número da federação partidária[cite: 4]. | Número da federação ou `-1` |
| **NM_FEDERACAO** | Texto | Nome da federação pela qual o partido concorre[cite: 4]. | Ex: `Federação PSDB CIDADANIA` ou `#NULO` |
| **SG_FEDERACAO** | Texto | Sigla da federação partidária[cite: 4]. | Ex: `45-PSDB/23-CIDADANIA` ou `#NULO` |
| **DS_COMPOSICAO_FEDERACAO** | Texto | Composição dos partidos federados (separados por `/`)[cite: 4]. | Ex: `45-PSDB/23-CIDADANIA` ou `#NULO` |
| **SQ_COLIGACAO** | Numérico | Sequencial único da coligação na Justiça Eleitoral[cite: 4]. | Código sequencial numérico[cite: 4] |
| **NM_COLIGACAO** | Texto | Nome oficial da coligação[cite: 4]. | Texto com a denominação da coligação |
| **DS_COMPOSICAO_COLIGACAO** | Texto | Composição das siglas dos partidos/federações na coligação[cite: 4]. | Texto intercalado com `/` ou `,`[cite: 4] |



### 2.5. Situação e Votação da Legenda

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_SITUACAO_LEGENDA** | Texto/Numérico | Código da situação da legenda/agremiação[cite: 4]. | Ex: `D` (Deferido), `I` (Indeferido), etc. |
| **DS_SITUACAO** | Texto | Descrição da situação da legenda[cite: 4]. | Ex: `DEFERIDO`, `INDEFERIDO`, `EM JULGAMENTO` |
| **NM_TIPO_DESTINACAO_VOTOS** | Texto | Nome do tipo da destinação dos votos atribuídos à legenda[cite: 4]. | Ex: `Válido`, `Anulado`, `#NE` |