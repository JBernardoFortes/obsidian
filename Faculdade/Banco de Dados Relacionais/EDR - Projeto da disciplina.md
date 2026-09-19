
Fazer o EDR da API do TSE e das apis necessarias para puxar os dados das analises do projeto final

Tabelas mandadas pelo J Carlos:

### Candidato

| NR_CPF_CANDIDATO | NM_CANDIDATO | DT_NASCIMENTO | DS_GRAU_INSTRUCAO | DS_GENERO | DS_COR_RACA |
| ---------------- | ------------ | ------------- | ----------------- | --------- | ----------- |
|                  |              |               |                   |           |             |

## Candidatura ( Entidade Fraca / Evento )

| SQ_CANDIDATO | NR_CPF_CANDIDATO | CD_MUNICIPIO_TSE | SG_PARTIDO | ANO_ELEICAO | DS_CARGO | DS_SIT_TOT_TURNO |
| ------------ | ---------------- | ---------------- | ---------- | ----------- | -------- | ---------------- |
|              |                  |                  |            |             |          |                  |

### Bens_Declarados

| ID_BEM | SQ_CANDIDATO | DS_TIPO_BEM | DS_BEM | VR_BEM |
| ------ | ------------ | ----------- | ------ | ------ |
|        |              |             |        |        |

### Receitas_Campanha

| ID_RECEITA | SQ_CANDIDATO | DS_FONTE_RECEITA | VR_RECEITA |
| ---------- | ------------ | ---------------- | ---------- |
|            |              |                  |            |

### Despesas_Pagas

| ID_DESPESA | SQ_CANDIDATO | DS_DESPESA | VR_PAGO |
| ---------- | ------------ | ---------- | ------- |
|            |              |            |         |

### Plano_Governo

| SQ_CANDIDATO | TXT_PROPOSTA |
| ------------ | ------------ |
|              |              |

### Municipio

| CD_MUNICIPIO_TSE | CD_MUNICIPIO_IBGE | NM_MUNICIPIO | SG_UF | PIB_PER_CAPITA | IDHM | POPULACAO_TOTAL |
| ---------------- | ----------------- | ------------ | ----- | -------------- | ---- | --------------- |
|                  |                   |              |       |                |      |                 |

### Perfil_Eleitorado

| CD_MUNICIPIO_TSE | ANO_ELEICAO | DS_FAIXA_ETARIA | QT_ELEITORES |
| ---------------- | ----------- | --------------- | ------------ |
|                  |             |                 |              |

### Partido

| SG_PARTIDO | NM_PARTIDO | VIES_POLITICO |     |
| ---------- | ---------- | ------------- | --- |
|            |            |               |     |

