# Dicionário de Dados - Tabela FATO_IDHM_ATLAS

Armazena os dados do Índice de Desenvolvimento Humano Municipal (IDHM) extraídos do Atlas do Desenvolvimento Humano.



## Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CODMUN7** | Texto | Código IBGE de 7 dígitos do município (Chave Estrangeira). | Código IBGE de 7 dígitos |
| **ANO_REFERENCIA** | Numérico | Ano do Censo Demográfico de referência dos dados. | `1991`, `2000`, `2010` |
| **IDHM** | Decimal | Índice de Desenvolvimento Humano Municipal (Geral). | `0,000` a `1,000` |
| **IDHM_R** | Decimal | Dimensão Renda do IDHM. | `0,000` a `1,000` |
| **IDHM_L** | Decimal | Dimensão Longevidade do IDHM. | `0,000` a `1,000` |
| **IDHM_E** | Decimal | Dimensão Educação do IDHM. | `0,000` a `1,000` |
[[Tabelas]]