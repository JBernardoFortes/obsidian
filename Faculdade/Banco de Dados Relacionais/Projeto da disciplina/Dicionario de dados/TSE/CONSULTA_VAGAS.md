[[TSE]]

## 1. Considerações e Regras Gerais

* **Codificação de Caracteres:** `Latin 1` (ISO-8859-1)[cite: 5].
* **Delimitador de Campos:** Ponto e vírgula (`;`)[cite: 5].
* **Qualificador de Texto:** Aspas ( `" "` ) em todos os campos (inclusive numéricos)[cite: 5].
* **Valores Especiais / Ausentes:**
  * `#NULO` (texto) ou `-1` (numérico): Informação em branco no banco de dados[cite: 5].
  * `#NE` (texto) ou `-3` (numérico): Não existente / Não registrado naquele ano eleitoral[cite: 5].
* **Valores Especiais para UF (Sigla do Estado):**
  * `BR`: Âmbito nacional[cite: 5].
  * `VT`: Voto em trânsito[cite: 5].
  * `ZZ`: Exterior[cite: 5].

### Esta tabela contém as informações oficiais sobre a **quantidade de vagas eleitorais disponíveis** em cada município.

## 2. Dicionário dos Campos

### 2.1. Controle e Identificação da Extração

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **DT_GERACAO** | Data | Data da extração dos dados para geração do arquivo[cite: 5]. | DD/MM/AAAA |
| **HH_GERACAO** | Hora | Hora da extração dos dados com base no horário de Brasília[cite: 5]. | HH:MM:SS |
| **ANO_ELEICAO** | Numérico | Ano de referência da eleição para geração do arquivo[cite: 5]. | AAAA |


### 2.2. Dados da Eleição e Posse

| Variável            | Tipo     | Descrição                                                                          | Domínio / Valores Possíveis                                                          |
| :------------------ | :------- | :--------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------- |
| **CD_TIPO_ELEICAO** | Numérico | Código do tipo de eleição[cite: 5].                                                | `1`: Eleição Suplementar<br>`2`: Eleição Ordinária<br>`3`: Consulta Popular[cite: 5] |
| **NM_TIPO_ELEICAO** | Texto    | Nome/Descrição do tipo de eleição[cite: 5].                                        | Ex: `Eleição Ordinária`, `Eleição Suplementar`, `Consulta Popular`[cite: 5]          |
| **CD_ELEICAO**      | Numérico | Código único da eleição no âmbito da Justiça Eleitoral (único por turno)[cite: 5]. | Código numérico único                                                                |
| **DS_ELEICAO**      | Texto    | Descrição da eleição[cite: 5].                                                     | Ex: `Eleições Municipais 2024`                                                       |
| **DT_ELEICAO**      | Data     | Data da ocorrência da eleição[cite: 5].                                            | DD/MM/AAAA                                                                           |
| **DT_POSSE**        | Data     | Data de posse para o cargo em disputa[cite: 5].                                    | DD/MM/AAAA (ex: `01/01/2025`)                                                        |


### 2.3. Localidade, Cargo e Vagas

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SG_UF** | Texto | Sigla da Unidade da Federação em que se realizam as eleições[cite: 5]. | Siglas das UFs, `BR`, `VT` ou `ZZ`[cite: 5] |
| **SG_UE** | Texto/Numérico | Sigla da Unidade Eleitoral (UF em âmbito estadual/nacional ou Código TSE do município em âmbito municipal)[cite: 5]. | Ex: `BR`, Sigla da UF ou Código do Município[cite: 5] |
| **NM_UE** | Texto | Nome da Unidade Eleitoral (Nome do município, da UF ou "Brasil")[cite: 5]. | Ex: `"MONTADAS"`, Nome da UF ou `"Brasil"`[cite: 5] |
| **CD_CARGO** | Numérico | Código do cargo ao qual a vaga se destina[cite: 5]. | Ex: `11` (Prefeito), `12` (Vice-Prefeito), `13` (Vereador) |
| **DS_CARGO** | Texto | Descrição do cargo ao qual a vaga se destina[cite: 5]. | Ex: `Prefeito`, `Vice-prefeito`, `Vereador` |
| **QT_VAGA** | Numérico | Quantidade de vagas disponíveis para aquele cargo, agrupadas por unidade eleitoral[cite: 5]. | Número inteiro positivo (ex: `1`, `9`, `11`, `15`) |
