# Dicionário de Dados - Tabela DIM_MUNICIPIO

Centraliza a identificação dos municípios e integra as chaves territoriais do TSE e do IBGE.



## Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_MUNICIPIO_IBGE** | Texto | Código oficial do município no IBGE (Chave Primária). | Código IBGE de 7 dígitos |
| **SG_UE** | Texto | Sigla/Código do município no TSE (Unidade Eleitoral). | Código TSE ou Sigla da UF |
| **NM_MUNICIPIO** | Texto | Nome oficial do município. | Nome do município |
| **SG_UF** | Texto | Sigla da Unidade da Federação. | `AC` ... `TO` |
[[Tabelas]]