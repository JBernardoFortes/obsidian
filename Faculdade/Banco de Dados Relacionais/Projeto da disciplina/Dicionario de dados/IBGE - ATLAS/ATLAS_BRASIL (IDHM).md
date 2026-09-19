[[IBGE - ATLAS]]
# Dicionário de Dados - Tabela ATLAS_BRASIL (IDHM)

Este dicionário descreve a estrutura dos dados do Índice de Desenvolvimento Humano Municipal (IDHM) extraídos do Atlas do Desenvolvimento Humano no Brasil (PNUD, Ipea e Fundação João Pinheiro)[cite: 8].



## 1. Considerações e Regras Gerais

* **Fonte Oficial:** Atlas do Desenvolvimento Humano no Brasil (PNUD, Ipea e Fundação João Pinheiro)[cite: 8].
* **Nível Territorial:** Municipal[cite: 8].
* **Chave Primária de Ligação:** `CODMUN7` (código de 7 dígitos do município), podendo ser associado ao `CD_MUNICIPIO_IBGE` mantendo a validação de município e UF[cite: 8].
* **Cobertura Temporal:** Censos Demográficos de `1991`, `2000` e `2010`[cite: 8].
* **Periodicidade:** **Não é uma série anual**[cite: 8]. O IDHM municipal não possui dados para anos intercensitários (ex: 2012, 2016, 2020, 2022, 2024)[cite: 8].
* **Regra Temporal do Projeto:** Para análises ligadas a eleições recentes (como 2024), utiliza-se o indicador mais recente disponível (`ANO_REFERENCIA_IDHM = 2010`), registrando-o explicitamente como *IDHM de referência 2010* e sem realizar interpolações artificiais[cite: 8].
* **Restrição:** O *Radar IDHM* não deve ser utilizado como substituto municipal anual[cite: 8].



## 2. Dicionário dos Campos

### 2.1. Identificação Territorial

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CODMUN7** | Texto | Código municipal de 7 dígitos utilizado pelo Atlas/IBGE[cite: 8]. | Código IBGE de 7 dígitos[cite: 8] |
| **NM_MUNICIPIO** | Texto | Nome oficial do município[cite: 8]. | Nome do município[cite: 8] |
| **UF** | Texto/Numérico | Identificação da Unidade da Federação (sigla ou código)[cite: 8]. | Sigla/Código da UF[cite: 8] |
| **ANO_REFERENCIA** | Numérico | Ano do Censo Demográfico de referência dos dados[cite: 8]. | `1991`, `2000`, `2010`[cite: 8] |



### 2.2. Índices de Desenvolvimento Humano (IDHM)

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **IDHM** | Decimal | Índice de Desenvolvimento Humano Municipal (Geral)[cite: 8]. | `0,000` a `1,000`[cite: 8] |
| **IDHM_R** | Decimal | Dimensão Renda do IDHM (Capacidade de prover padrão digno de vida)[cite: 8]. | `0,000` a `1,000`[cite: 8] |
| **IDHM_L** | Decimal | Dimensão Longevidade do IDHM (Oportunidade de viver uma vida longa e saudável)[cite: 8]. | `0,000` a `1,000`[cite: 8] |
| **IDHM_E** | Decimal | Dimensão Educação do IDHM (Acesso ao conhecimento)[cite: 8]. | `0,000` a `1,000`[cite: 8] |



## 3. Faixas de Classificação do IDHM

Caso a aplicação exiba a classificação qualitativa oficial do Atlas do Desenvolvimento Humano[cite: 8]:

| Faixa de Desenvolvimento | Intervalo de Valor |
| :--- | :--- |
| **Muito Baixo** | `0,000` a `0,499`[cite: 8] |
| **Baixo** | `0,500` a `0,599`[cite: 8] |
| **Médio** | `0,600` a `0,699`[cite: 8] |
| **Alto** | `0,700` a `0,799`[cite: 8] |
| **Muito Alto** | `0,800` a `1,000`[cite: 8] |



## 4. Informações Contidas nesta Tabela

A tabela reúne os dados históricos do **Índice de Desenvolvimento Humano Municipal (IDHM)** de todos os municípios brasileiros com base nas apurações censitárias[cite: 8].

 Ela permite avaliar o nível de desenvolvimento humano da população municipal sob **três dimensões fundamentais**[cite: 8]:
1. **Renda (`IDHM_R`):** Mede a renda per capita média do município[cite: 8].
2. **Longevidade (`IDHM_L`):** Mede a esperança de vida ao nascer[cite: 8].
3. **Educação (`IDHM_E`):** Mede a escolaridade da população adulta e o fluxo escolar dos jovens[cite: 8].

### Principais limitações a considerar:
* Não existem dados anuais; o último IDHM municipal disponível oficialmente na escala censitária é o do **Censo 2010**[cite: 8].
* Não se deve inferir ou interpolar valores para 2022 ou 2024[cite: 8].