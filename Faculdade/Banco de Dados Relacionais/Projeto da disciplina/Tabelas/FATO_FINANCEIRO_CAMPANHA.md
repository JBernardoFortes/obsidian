# Dicionário de Dados - Tabela FATO_FINANCEIRO_CAMPANHA

Registra os valores financeiros de despesas, doações e gastos de campanha do candidato.



## Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SQ_CANDIDATO** | Numérico | Sequencial do candidato (Chave Estrangeira). | Código sequencial do TSE |
| **ANO_ELEICAO** | Numérico | Ano da eleição. | `2018`, `2020`, `2022`, `2024` |
| **VR_DESPESA_CONTRATADA** | Decimal | Valor total de despesas contratadas na campanha. | Valor monetário em R$ |
| **VR_GASTO_PROPAGANDA** | Decimal | Valor total gasto especificamente com propaganda/mídia. | Valor monetário em R$ |
| **VR_RECEITA_PJ** | Decimal | Valor total de doações/recursos recebidos de Pessoas Jurídicas. | Valor monetário em R$ |
| **VR_DESPESA_MAX_CAMPANHA** | Decimal | Teto/limite máximo de gastos permitido para o cargo no município. | Valor monetário em R$ |
[[Tabelas]]