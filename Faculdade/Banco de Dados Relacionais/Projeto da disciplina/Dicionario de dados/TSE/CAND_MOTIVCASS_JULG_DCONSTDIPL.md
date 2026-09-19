
[[TSE]]
## 1. Considerações e Regras Gerais

* **Codificação de Caracteres:** `Latin 1` (ISO-8859-1)[cite: 6].
* **Delimitador de Campos:** Ponto e vírgula (`;`)[cite: 6].
* **Qualificador de Texto:** Aspas ( `" "` ) em todos os campos (inclusive numéricos)[cite: 6].
* **Valores Especiais / Ausentes:**
  * `#NULO` (texto) ou `-1` (numérico): Informação em branco no banco de dados[cite: 6].
  * `#NE` (texto) ou `-3` (numérico): Não existente / Não registrado naquele ano eleitoral[cite: 6].
* **Valores Especiais para UF (Sigla do Estado):**
  * `BR`: Âmbito nacional[cite: 6].
  * `VT`: Voto em trânsito[cite: 6].
  * `ZZ`: Exterior[cite: 6].

### Esta tabela  reúne as informações oficiais sobre os **motivos de indeferimento de registo de candidatura, cassação de mandato ou desconstituição de diploma** referentes às Eleições.


## 2. Dicionário dos Campos

### 2.1. Controle e Identificação da Extração

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DT_GERACAO** | Data | Data da extração dos dados para geração do arquivo[cite: 6]. | DD/MM/AAAA |
| **HH_GERACAO** | Hora | Hora da extração dos dados com base no horário de Brasília[cite: 6]. | HH:MM:SS |
| **ANO_ELEICAO** | Numérico | Ano de referência da eleição para geração do arquivo[cite: 6]. | AAAA |



### 2.2. Dados da Eleição

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_TIPO_ELEICAO** | Numérico | Código do tipo de eleição[cite: 6]. | `1`: Eleição Suplementar<br>`2`: Eleição Ordinária<br>`3`: Consulta Popular[cite: 6] |
| **NM_TIPO_ELEICAO** | Texto | Nome/Descrição do tipo de eleição[cite: 6]. | Ex: `Eleição Ordinária`, `Eleição Suplementar`, `Consulta Popular`[cite: 6] |
| **CD_ELEICAO** | Numérico | Código único da eleição no âmbito da Justiça Eleitoral (único por turno)[cite: 6]. | Código numérico único |
| **DS_ELEICAO** | Texto | Descrição da eleição[cite: 6]. | Ex: `Eleições Municipais 2024`[cite: 6] |



### 2.3. Localidade e Candidato

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SG_UF** | Texto | Sigla da Unidade da Federação na qual o candidato concorre[cite: 6]. | Siglas das UFs, `BR`, `VT` ou `ZZ`[cite: 6] |
| **SG_UE** | Texto/Numérico | Sigla da Unidade Eleitoral (UF em âmbito estadual/nacional ou Código TSE do município em âmbito municipal)[cite: 6]. | Ex: `BR`, Sigla da UF ou Código do Município[cite: 6] |
| **NM_UE** | Texto | Nome da Unidade Eleitoral (Nome do município, da UF ou "Brasil")[cite: 6]. | Ex: `"LUÍS EDUARDO MAGALHÃES"`, Nome da UF ou `"Brasil"`[cite: 6] |
| **SQ_CANDIDATO** | Numérico | Número sequencial do candidato gerado internamente pelos sistemas eleitorais[cite: 6]. | Código sequencial único do TSE[cite: 6] |
| **NR_PROCESSO** | Numérico/Texto | Número do processo judicial no PJe de registro de candidatura, cassação ou desconstituição de diploma. | Número do processo único |


### 2.4. Motivação e Fundamentação do Julgamento

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DS_TP_MOTIVO** | Texto | Descrição do tipo do motivo (indica se é relativo a julgamento do registro, cassação ou desconstituição de diploma)[cite: 6]. | Ex: `Fundamentos legais de julgamento` |
| **DS_MOTIVO** | Texto | Descrição detalhada do motivo que ocasionou o indeferimento do registro, a cassação ou a desconstituição de diploma[cite: 6]. | Ex: `Ausência de condição de elegibilidade`, `Incidência em causa de inelegibilidade` |