[[TSE]]
## 1. Considerações e Regras Gerais

* **Codificação de Caracteres:** `Latin 1` (ISO-8859-1).
* **Delimitador de Campos:** Ponto e vírgula (`;`).
* **Qualificador de Texto:** Aspas ( `" "` ) em todos os campos (inclusive numéricos)[cite: 7].
* **Valores Especiais / Ausentes:**
  * `#NULO` (texto) ou `-1` (numérico): Informação em branco no banco de dados[cite: 7].
  * `#NE` (texto) ou `-3` (numérico): Não existente / Não registrado naquele ano eleitoral[cite: 7].
* **Valores Especiais para UF (Sigla do Estado):**
  * `BR`: Âmbito nacional[cite: 7].
  * `VT`: Voto em trânsito[cite: 7].
  * `ZZ`: Exterior[cite: 7].

A tabela  reúne todos os **endereços eletrónicos, redes sociais e canais digitais oficiais declarados à Justiça Eleitoral** pelos candidatos que disputaram as **Eleições Municipais de 2024.

## 2. Dicionário dos Campos

### 2.1. Controle e Identificação da Extração

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DT_GERACAO** | Data | Data da extração dos dados para geração do arquivo[cite: 7]. | DD/MM/AAAA |
| **HH_GERACAO** | Hora | Hora da extração dos dados com base no horário de Brasília[cite: 7]. | HH:MM:SS |
| **AA_ELEICAO** / **ANO_ELEICAO** | Numérico | Ano de referência da eleição para geração do arquivo[cite: 7]. | AAAA |



### 2.2. Dados da Eleição

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_TIPO_ELEICAO** | Numérico | Código do tipo de eleição[cite: 7]. | `1`: Eleição Suplementar<br>`2`: Eleição Ordinária<br>`3`: Consulta Popular[cite: 7] |
| **NM_TIPO_ELEICAO** | Texto | Nome/Descrição do tipo de eleição[cite: 7]. | Ex: `ELEIÇÃO ORDINÁRIA`, `ELEIÇÃO SUPLEMENTAR`, `CONSULTA POPULAR`[cite: 7] |
| **CD_ELEICAO** | Numérico | Código único da eleição no âmbito da Justiça Eleitoral (único por turno)[cite: 7]. | Código numérico único |
| **DS_ELEICAO** | Texto | Descrição do pleito eleitoral[cite: 7]. | Ex: `ELEIÇÕES MUNICIPAIS 2024`[cite: 7] |
| **SG_UF** | Texto | Sigla da Unidade da Federação na qual o candidato concorre[cite: 7]. | Siglas das UFs, `BR`, `VT` ou `ZZ`[cite: 7] |


### 2.3. Identificação e Redes Sociais do Candidato

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SQ_CANDIDATO** | Numérico | Número sequencial do candidato gerado internamente pelos sistemas eleitorais[cite: 7]. | Código sequencial único do TSE[cite: 7] |
| **NR_ORDEM_REDE_SOCIAL** | Numérico | Número de ordenação da rede social declarada pelo candidato[cite: 7]. | Número sequencial (1, 2, 3, ...)[cite: 7] |
| **DS_URL** | Texto | Endereço WEB / Link direto para o perfil ou canal digital do candidato[cite: 7]. | URL da rede social ou website oficial |