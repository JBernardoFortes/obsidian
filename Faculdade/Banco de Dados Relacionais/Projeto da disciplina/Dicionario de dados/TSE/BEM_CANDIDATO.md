
[[TSE]]

## 1. Considerações e Regras Gerais

* **Codificação de Caracteres:** `Latin 1` (ISO-8859-1)[cite: 3].
* **Delimitador de Campos:** Ponto e vírgula (`;`)[cite: 3].
* **Qualificador de Texto:** Aspas ( `" "` ) em todos os campos (inclusive numéricos)[cite: 3].
* **Valores Especiais / Ausentes:**
  * `#NULO` (texto) ou `-1` (numérico): Informação em branco no banco de dados[cite: 3].
  * `#NE` (texto) ou `-3` (numérico): Não existente / Não registrado naquele ano eleitoral[cite: 3].
* **Valores Especiais para UF (Sigla do Estado):**
  * `BR`: Âmbito nacional[cite: 3].
  * `VT`: Voto em trânsito[cite: 3].
  * `ZZ`: Exterior[cite: 3].
  
### Essa tabela possui os dados dos bens dos candidatos



## 2. Dicionário dos Campos

### 2.1. Controle e Identificação da Extração

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DT_GERACAO** | Data | Data da extração dos dados para geração do arquivo[cite: 3]. | DD/MM/AAAA |
| **HH_GERACAO** | Hora | Hora da extração dos dados com base no horário de Brasília[cite: 3]. | HH:MM:SS |
| **ANO_ELEICAO** | Numérico | Ano de referência da eleição para geração do arquivo[cite: 3]. | AAAA |



### 2.2. Dados da Eleição

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_TIPO_ELEICAO** | Numérico | Código do tipo de eleição[cite: 3]. | `1`: Eleição Suplementar<br>`2`: Eleição Ordinária<br>`3`: Consulta Popular[cite: 3] |
| **NM_TIPO_ELEICAO** | Texto | Nome/Descrição do tipo de eleição[cite: 3]. | Ex: `Eleição Ordinária`, `Eleição Suplementar`, `Consulta Popular`[cite: 3] |
| **CD_ELEICAO** | Numérico | Código único da eleição no âmbito da Justiça Eleitoral (único por turno)[cite: 3]. | Código numérico único |
| **DS_ELEICAO** | Texto | Descrição da eleição[cite: 3]. | Ex: `Eleições Municipais 2024` |
| **DT_ELEICAO** | Data | Data de ocorrência da eleição[cite: 3]. | DD/MM/AAAA |



### 2.3. Localidade e Candidato

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SG_UF** | Texto | Sigla da Unidade da Federação na qual o candidato concorre[cite: 3]. | Siglas das UFs, `BR`, `VT` ou `ZZ`[cite: 3] |
| **SG_UE** | Texto/Numérico | Sigla da Unidade Eleitoral (UF em âmbito estadual/nacional ou Código TSE do município em âmbito municipal)[cite: 3]. | Ex: `BR`, Sigla da UF ou Código do Município[cite: 3] |
| **NM_UE** | Texto | Nome da Unidade Eleitoral (Nome do município, da UF ou "Brasil")[cite: 3]. | Ex: `"NITERÓI"`, Nome da UF ou `"Brasil"`[cite: 3] |
| **SQ_CANDIDATO** | Numérico | Número sequencial do candidato gerado internamente pelos sistemas eleitorais[cite: 3]. | Código sequencial único do TSE[cite: 3] |



### 2.4. Detalhamento do Bem Patrimonial

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **NR_ORDEM_BEM_CANDIDATO** | Numérico | Número de ordenação do bem patrimonial segundo a sequência declarada pelo candidato[cite: 3]. | Número sequencial (1, 2, 3, ...)[cite: 3] |
| **CD_TIPO_BEM_CANDIDATO** | Numérico | Código do tipo do bem patrimonial material declarado[cite: 3]. | Código numérico de classificação do bem |
| **DS_TIPO_BEM_CANDIDATO** | Texto | Descrição da categoria/tipo do bem patrimonial[cite: 3]. | Ex: `Predio residencial`, `Veículo automotor terrestre`, `Caderneta de poupança` |
| **DS_BEM_CANDIDATO** | Texto | Descrição detalhada do bem material patrimonial do candidato[cite: 3]. | Texto explicativo informado pelo candidato |
| **VR_BEM_CANDIDATO** | Decimal | Valor, em reais, do bem patrimonial material declarado[cite: 3]. | Valor numérico monetário (ex: `45000,00`) |
| **DT_ULT_ATUAL_BEM_CANDIDATO** | Data | Data da última atualização do bem no sistema do TSE[cite: 3]. | DD/MM/AAAA |
| **HH_ULT_ATUAL_BEM_CANDIDATO** | Hora | Hora da última atualização do bem no sistema do TSE[cite: 3]. | HH:MM:SS |