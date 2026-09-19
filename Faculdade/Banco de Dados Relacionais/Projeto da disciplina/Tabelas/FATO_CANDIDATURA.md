# Dicionário de Dados - Tabela FATO_CANDIDATURA

Modela a participação de um candidato em determinado ano, eleição, cargo e município.

---

## Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SQ_CANDIDATO** | Numérico | Sequencial do candidato (Chave Estrangeira). | Código sequencial do TSE |
| **ANO_ELEICAO** | Numérico | Ano de referência do pleito eleitoral. | `2018`, `2020`, `2022`, `2024` |
| **CD_ELEICAO** | Numérico | Código único da eleição/turno no TSE. | Código numérico |
| **NR_TURNO** | Numérico | Turno do pleito eleitoral. | `1`, `2` |
| **CD_MUNICIPIO_IBGE** | Texto | Código IBGE do município (Chave Estrangeira). | Código IBGE de 7 dígitos |
| **NR_PARTIDO** | Numérico | Número do partido pelo qual concorre (Chave Estrangeira). | Número do partido |
| **CD_CARGO** | Numérico | Código do cargo disputado. | Ex: `11` (Prefeito), `13` (Vereador) |
| **DS_CARGO** | Texto | Descrição do cargo disputado. | Ex: `PREFEITO`, `VEREADOR`, `DEPUTADO` |
| **CD_SIT_TOT_TURNO** | Numérico | Código do resultado/situação final do candidato no turno. | Código numérico |
| **DS_SIT_TOT_TURNO** | Texto | Situação final do candidato no turno. | `ELEITO`, `NÃO ELEITO`, `SUPLENTE`, `2º TURNO` |
| **ST_REELEICAO** | Texto | Indica se concorre à reeleição para o mesmo cargo. | `S`: Sim, `N`: Não |
| **ST_DECLARAR_BENS** | Texto | Indica se declarou bens patrimoniais. | `S`: Sim, `N`: Não |
[[Tabelas]]