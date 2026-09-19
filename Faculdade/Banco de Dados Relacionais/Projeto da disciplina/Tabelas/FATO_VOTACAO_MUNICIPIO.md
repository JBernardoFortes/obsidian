# Dicionário de Dados - Tabela FATO_VOTACAO_MUNICIPIO

Consolida as estatísticas municipais de eleitorado, votação por legenda e abstenção.



##  Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_MUNICIPIO_IBGE** | Texto | Código IBGE do município (Chave Estrangeira). | Código IBGE de 7 dígitos |
| **ANO_ELEICAO** | Numérico | Ano da eleição. | `2018`, `2020`, `2022`, `2024` |
| **QT_ELEITORES** | Numérico | Quantidade total de eleitores aptos a votar no município. | Número inteiro |
| **QT_VOTOS_NOMINAIS** | Numérico | Quantidade de votos dados diretamente aos candidatos. | Número inteiro |
| **QT_VOTOS_LEGENDA** | Numérico | Quantidade de votos dados diretamente aos partidos/legendas. | Número inteiro |
| **QT_ABSTENCAO** | Numérico | Quantidade de eleitores que não compareceram às urnas. | Número inteiro |
| **PCT_ABSTENCAO** | Decimal | Taxa percentual de abstenção municipal (`QT_ABSTENCAO / QT_ELEITORES`). | `0` a `100%` |
[[Tabelas]]