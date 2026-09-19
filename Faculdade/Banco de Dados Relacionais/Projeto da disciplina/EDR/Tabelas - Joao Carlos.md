[[EDR - Projeto da disciplina]]


Tabelas mandadas pelo J Carlos:

### Candidato

| NR_CPF_CANDIDATO | NM_CANDIDATO | DT_NASCIMENTO | DS_GRAU_INSTRUCAO | DS_GENERO | DS_COR_RACA |
| ---------------- | ------------ | ------------- | ----------------- | --------- | ----------- |
| TEXT ( PK )      | TEXT         | TEXT          | TEXT              | TEXT      | TEXT        |
|                  |              |               |                   |           |             |

## Candidatura ( Entidade Fraca / Evento )

| SQ_CANDIDATO | NR_CPF_CANDIDATO | CD_MUNICIPIO_TSE | SG_PARTIDO  | ANO_ELEICAO | DS_CARGO | DS_SIT_TOT_TURNO |
| ------------ | ---------------- | ---------------- | ----------- | ----------- | -------- | ---------------- |
| INT ( PK )   | TEXT ( FK )      | TEXT ( FK )      | TEXT ( FK ) | INT         | TEXT     | TEXT             |
|              |                  |                  |             |             |          |                  |

### Bens_Declarados

| ID_BEM     | SQ_CANDIDATO | DS_TIPO_BEM | DS_BEM | VR_BEM |
| ---------- | ------------ | ----------- | ------ | ------ |
| INT ( PK ) | INT ( FK )   | TEXT        | TEXT   | TEXT   |

### Receitas_Campanha

| ID_RECEITA | SQ_CANDIDATO | DS_FONTE_RECEITA | VR_RECEITA |
| ---------- | ------------ | ---------------- | ---------- |
| INT ( PK ) | INT ( FK )   | TEXT             | TEXT       |

### Despesas_Pagas

| ID_DESPESA | SQ_CANDIDATO | DS_DESPESA | VR_PAGO |
| ---------- | ------------ | ---------- | ------- |
| INT ( PK ) | ID ( FK )    | TEXT       | TEXT    |

### Plano_Governo

| ID         | SQ_CANDIDATO | TXT_PROPOSTA |
| ---------- | ------------ | ------------ |
| INT ( PK ) | INT ( FK )   | TEXT         |

### Municipio

| CD_MUNICIPIO_TSE | CD_MUNICIPIO_IBGE | NM_MUNICIPIO | SG_UF | PIB_PER_CAPITA | IDHM | POPULACAO_TOTAL |
| ---------------- | ----------------- | ------------ | ----- | -------------- | ---- | --------------- |
| INT ( PK )       | INT               | TEXT         | TEXT  | TEXT           | TEXT | INT             |

### Perfil_Eleitorado

| CD_MUNICIPIO_TSE | ANO_ELEICAO | DS_FAIXA_ETARIA | QT_ELEITORES |
| ---------------- | ----------- | --------------- | ------------ |
| TEXT ( PK )      | TEXT ( PK ) | TEXT ( PK )     | INT          |

### Partido

| SG_PARTIDO | NM_PARTIDO | VIES_POLITICO      |
| ---------- | ---------- | ------------------ |
| INT ( PK ) | TEXT       | TEXT ( A decidir ) |

### Votacao_Partido

| CD_MUNICIPIO_TSE | ANO_ELEICAO | SG_PARTIDO  | QT_VOTOS_LEGENDA | QT_VOTOS_NOMINAIS |
| ---------------- | ----------- | ----------- | ---------------- | ----------------- |
| TEXT ( PK / FK ) | TEXT ( FK ) | TEXT ( FK ) | INT              | INT               |
|                  |             |             |                  |                   |
