# Dicionário de Dados - Tabela DIM_PARTIDO

Armazena os dados cadastrais dos partidos políticos e a sua classificação de orientação/viés político.



## Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **NR_PARTIDO** | Numérico | Número oficial do partido político (Chave Primária). | Ex: `13`, `22`, `15`, `45` |
| **SG_PARTIDO** | Texto | Sigla oficial do partido. | Ex: `PT`, `PL`, `MDB`, `PSDB` |
| **NM_PARTIDO** | Texto | Nome completo do partido político. | Texto |
| **VIES_POLITICO** | Texto | Orientação/viés político classificado metodologicamente pelo projeto. | `Esquerda`, `Centro-Esquerda`, `Centro`, `Centro-Direita`, `Direita` |
[[Tabelas]]