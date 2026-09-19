# Dicionário de Dados - Tabela DIM_CANDIDATO

Entidade centralizadora do perfil demográfico e pessoal único do candidato.



## Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **SQ_CANDIDATO** | Numérico | Sequencial único do candidato gerado pelo TSE (Chave Primária). | Sequencial numérico do TSE |
| **NM_CANDIDATO** | Texto | Nome completo do candidato. | Texto |
| **NM_URNA_CANDIDATO** | Texto | Nome do candidato exibido na urna eleitoral. | Texto |
| **CD_GENERO** | Numérico | Código do gênero do candidato. | `2`: Masculino, `4`: Feminino |
| **DS_GENERO** | Texto | Descrição do gênero. | `MASCULINO`, `FEMININO` |
| **CD_GRAU_INSTRUCAO** | Numérico | Código do grau de escolaridade. | `1` a `8` |
| **DS_GRAU_INSTRUCAO** | Texto | Descrição do grau de instrução. | Ex: `ENSINO MÉDIO COMPLETO`, `SUPERIOR COMPLETO` |
| **CD_COR_RACA** | Numérico | Código da cor/raça (padrão IBGE). | `01` a `06` |
| **DS_COR_RACA** | Texto | Autodeclaração de cor ou raça. | `BRANCA`, `PRETA`, `PARDA`, `AMARELA`, `INDÍGENA` |
| **DT_NASCIMENTO** | Data | Data de nascimento do candidato. | DD/MM/AAAA ou Vazio |
| **CD_NACIONALIDADE** | Numérico | Código da nacionalidade. | `1`: Brasileira nata, `2`: Naturalizada, etc. |
| **DS_NACIONALIDADE** | Texto | Descrição da nacionalidade. | Texto |

[[Tabelas]]