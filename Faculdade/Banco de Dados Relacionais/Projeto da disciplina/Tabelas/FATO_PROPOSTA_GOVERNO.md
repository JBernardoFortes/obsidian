# Dicionário de Dados - Tabela FATO_PROPOSTA_GOVERNO

Mapeia o conteúdo dos planos de governo apresentados pelos candidatos nas eleições majoritárias.



## Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SQ_CANDIDATO** | Numérico | Sequencial do candidato (Chave Estrangeira). | Código sequencial do TSE |
| **ANO_ELEICAO** | Numérico | Ano da eleição. | `2018`, `2020`, `2022`, `2024` |
| **DS_PROPOSTA_TEXTO** | Texto | Conteúdo/resumo extraído do arquivo do plano de governo. | Texto longo |
| **EIXO_TEMATICO** | Texto | Eixo/categoria temática da proposta. | Ex: `Educação`, `Saúde`, `Segurança`, `Economia` |
[[Tabelas]]