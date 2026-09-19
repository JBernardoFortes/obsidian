[[IBGE - ATLAS]]
# Dicionário de Dados - Tabela IBGE

Este dicionário descreve a estrutura dos dados socioeconômicos e demográficos municipais consolidados a partir do Instituto Brasileiro de Geografia e Estatística (IBGE), abrangendo sistemas como SIDRA, Censo Demográfico e a Base de Dados do PIB dos Municípios[cite: 9].



## 1. Considerações e Regras Gerais

* **Fonte Principal:** Instituto Brasileiro de Geografia e Estatística (IBGE)[cite: 9].
* **Sistemas de Origem:** SIDRA, Censo Demográfico e Base de Dados do PIB dos Municípios[cite: 9].
* **Chave Primária de Ligação:** `CD_MUNICIPIO_IBGE` (Código oficial do município no IBGE de 7 dígitos)[cite: 9].
* **Nível Territorial:** Municipal, salvo indicação em contrário[cite: 9].
* **Gestão Temporal:** O ano de referência do indicador socioeconômico deve ser armazenado separadamente do ano da eleição[cite: 9].
* **População:** Distinção obrigatória entre população censitária (`CENSITARIA`) e população estimada (`ESTIMADA`)[cite: 9].
* **PIB per capita:** Utilização do valor oficial divulgado pelo IBGE quando disponível, sem recalculação automática[cite: 9]. Para 2022 e 2023, considera os dados populacionais do Censo Demográfico 2022[cite: 9].
* **Valores Ausentes:** Normalização de dados ausentes/não publicados para `NULL` (preservando a omissão da fonte sem aplicar interpolação artificial)[cite: 9].
* **Limitações Conhecidas:** A abertura do VAB Setorial (Agropecuária, Indústria, Serviços, Administração Pública) está disponível na série histórica até 2021, não constando na divulgação recente de 2022 e 2023[cite: 9].



## 2. Dicionário dos Campos

### 2.1. Identificação do Município

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_MUNICIPIO_IBGE** | Texto | Código oficial do município no IBGE (preservar 7 dígitos)[cite: 9]. | Código IBGE de 7 dígitos[cite: 9] |
| **NM_MUNICIPIO** | Texto | Nome oficial do município[cite: 9]. | Nome do município[cite: 9] |
| **CD_UF** | Texto | Código da Unidade da Federação no IBGE[cite: 9]. | Código IBGE da UF[cite: 9] |
| **SG_UF** | Texto | Sigla da Unidade da Federação[cite: 9]. | `AC` ... `TO`[cite: 9] |
| **NM_UF** | Texto | Nome oficial da Unidade da Federação[cite: 9]. | Nome oficial da UF[cite: 9] |



### 2.2. População Municipal

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **ANO** | Numérico | Ano de referência da contagem/estimativa populacional[cite: 9]. | `AAAA`[cite: 9] |
| **POPULACAO** | Numérico | População residente no município[cite: 9]. | Número de habitantes[cite: 9] |
| **TIPO_POPULACAO** | Texto | Natureza do dado populacional[cite: 9]. | `CENSITARIA`, `ESTIMADA`[cite: 9] |
| **FONTE_POPULACAO** | Texto | Tabela ou base de origem utilizada[cite: 9]. | Ex: `IBGE_6579` (Estimativas), `IBGE_4714` (Censo 2022)[cite: 9] |



### 2.3. Produto Interno Bruto (PIB) Municipal

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **ANO** | Numérico | Ano de referência do PIB[cite: 9]. | `AAAA`[cite: 9] |
| **PIB** | Decimal | Produto Interno Bruto municipal a preços correntes[cite: 9]. | Valor monetário[cite: 9] |
| **UNIDADE_PIB** | Texto | Unidade monetária/escala apresentada pela fonte[cite: 9]. | Ex: `Mil Reais`[cite: 9] |
| **FONTE_PIB** | Texto | Fonte/tabela de origem do PIB[cite: 9]. | `SIDRA 5938`[cite: 9] |



### 2.4. PIB per capita Municipal

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **ANO** | Numérico | Ano de referência do PIB per capita[cite: 9]. | `AAAA`[cite: 9] |
| **PIB_PER_CAPITA** | Decimal | PIB per capita oficial do município[cite: 9]. | R$ por habitante[cite: 9] |
| **UNIDADE_PIB_PER_CAPITA** | Texto | Unidade monetária apresentada pela fonte[cite: 9]. | `R$ 1,00`[cite: 9] |
| **FONTE_PIB_PER_CAPITA** | Texto | Tabela/base utilizada[cite: 9]. | Base do PIB dos Municípios / IBGE[cite: 9] |



### 2.5. Área Territorial e Densidade Demográfica

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **AREA_KM2** | Decimal | Área territorial do município em quilómetros quadrados[cite: 9]. | Valor em km²[cite: 9] |
| **ANO_AREA** | Numérico | Ano de referência da área territorial[cite: 9]. | `AAAA`[cite: 9] |
| **FONTE_AREA** | Texto | Fonte do indicador de área[cite: 9]. | `IBGE`[cite: 9] |
| **DENSIDADE_HAB_KM2** | Decimal | Relação entre a população residente e a área territorial[cite: 9]. | habitantes/km²[cite: 9] |
| **ANO_DENSIDADE** | Numérico | Ano de referência da densidade demográfica[cite: 9]. | `AAAA`[cite: 9] |
| **FONTE_DENSIDADE** | Texto | Fonte do indicador de densidade demográfica[cite: 9]. | `IBGE`[cite: 9] |



### 2.6. Rendimento Domiciliar per capita

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **ANO** | Numérico | Ano de referência da renda[cite: 9]. | `AAAA`[cite: 9] |
| **RENDA_DOMICILIAR_PER_CAPITA** | Decimal | Rendimento domiciliar per capita do município[cite: 9]. | Valor monetário[cite: 9] |
| **UNIDADE_RENDA** | Texto | Unidade monetária da publicação[cite: 9]. | Conforme publicação oficial[cite: 9] |
| **FONTE_RENDA** | Texto | Tabela/base utilizada para a renda[cite: 9]. | `IBGE`[cite: 9] |



### 2.7. Estrutura e Faixas Etárias

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **ANO** | Numérico | Ano de referência da faixa etária[cite: 9]. | `AAAA`[cite: 9] |
| **FAIXA_ETARIA** | Texto | Faixa etária da população segundo a classificação oficial[cite: 9]. | Classificação oficial da fonte[cite: 9] |
| **POPULACAO_FAIXA_ETARIA** | Numérico | Quantidade absoluta de pessoas na faixa[cite: 9]. | Número de habitantes[cite: 9] |
| **PERCENTUAL_FAIXA_ETARIA** | Decimal | Participação percentual da faixa na população total[cite: 9]. | `0` a `100%`[cite: 9] |
| **FONTE_FAIXA_ETARIA** | Texto | Fonte utilizada para composição etária[cite: 9]. | `IBGE`[cite: 9] |



### 2.8. Variáveis Econômicas Setoriais (Opcionais)

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **VAB_AGROPECUARIA** | Decimal | Valor Adicionado Bruto da agropecuária (até 2021)[cite: 9]. | Valor monetário ou `NULL`[cite: 9] |
| **VAB_INDUSTRIA** | Decimal | Valor Adicionado Bruto da indústria (até 2021)[cite: 9]. | Valor monetário ou `NULL`[cite: 9] |
| **VAB_SERVICOS** | Decimal | Valor Adicionado Bruto de serviços, exceto administração pública (até 2021)[cite: 9]. | Valor monetário ou `NULL`[cite: 9] |
| **VAB_ADMINISTRACAO_PUBLICA** | Decimal | Valor Adicionado Bruto da administração, defesa, educação e saúde públicas e seguridade social (até 2021)[cite: 9]. | Valor monetário ou `NULL`[cite: 9] |



## 3. Classificação das Variáveis para o Projeto

* **Essenciais:** `POPULACAO`, `PIB`, `PIB_PER_CAPITA`[cite: 9]
* **Importantes:** `AREA_KM2`, `DENSIDADE_HAB_KM2`, `RENDA_DOMICILIAR_PER_CAPITA`, `FAIXA_ETARIA`[cite: 9]
* **Opcionais:** `VAB_AGROPECUARIA`, `VAB_INDUSTRIA`, `VAB_SERVICOS`, `VAB_ADMINISTRACAO_PUBLICA`[cite: 9]