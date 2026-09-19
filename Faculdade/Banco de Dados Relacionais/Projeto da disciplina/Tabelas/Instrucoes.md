
[[Tabelas]]
# Arquitetura Geral do Banco de Dados Relacional (TSE + IBGE + Atlas)

Este documento descreve a estrutura completa das tabelas do modelo de dados relacional projetado para o projeto, incluindo suas chaves primárias (PK), chaves estrangeiras (FK) e como elas se conectam para responder às análises eleitorais e socioeconômicas.



## 1. Visão Geral da Arquitetura


* **Tabelas de Dimensão (`DIM_`):** Armazenam entidades únicas com atributos cadastrais (Municípios, Candidatos e Partidos).
* **Tabelas Fato (`FATO_`):** Armazenam eventos, estatísticas, métricas financeiras, votos e dados temporais/socioeconômicos.



## 2. Estrutura Detalhada das Tabelas

### 2.1. Tabelas de Dimensão (Entidades Centrais)

#### `DIM_MUNICIPIO`
Tabela mestre de municípios. Faz a ponte de integração territorial entre a Justiça Eleitoral (TSE) e o IBGE.
* **`CD_MUNICIPIO_IBGE`** *(PK, VARCHAR(7))*: Código oficial de 7 dígitos do IBGE.
* **`SG_UE`** *(VARCHAR(10))*: Sigla/Código da Unidade Eleitoral no TSE (Código de município ou sigla de UF).
* **`NM_MUNICIPIO`** *(VARCHAR(100))*: Nome oficial do município.
* **`SG_UF`** *(VARCHAR(2))*: Sigla da Unidade da Federação.

#### `DIM_PARTIDO`
Tabela mestre de partidos políticos e seu enquadramento ideológico/político.
* **`NR_PARTIDO`** *(PK, INT)*: Número oficial do partido político (ex: 13, 22, 15).
* **`SG_PARTIDO`** *(VARCHAR(20))*: Sigla oficial (ex: PT, PL, MDB).
* **`NM_PARTIDO`** *(VARCHAR(100))*: Nome completo da agremiação partidária.
* **`VIES_POLITICO`** *(VARCHAR(20))*: Classificação do viés ideológico (`Esquerda`, `Centro-Esquerda`, `Centro`, `Centro-Direita`, `Direita`).

#### `DIM_CANDIDATO`
Tabela mestre com o perfil sociobiográfico e demográfico único de cada indivíduo.
* **`SQ_CANDIDATO`** *(PK, BIGINT)*: Número sequencial do candidato no TSE (único por pleito).
* **`NM_CANDIDATO`** *(VARCHAR(150))*: Nome completo.
* **`NM_URNA_CANDIDATO`** *(VARCHAR(150))*: Nome de urna/campanha.
* **`CD_GENERO`** *(INT)* / **`DS_GENERO`** *(VARCHAR(20))*: Código e descrição do gênero.
* **`CD_GRAU_INSTRUCAO`** *(INT)* / **`DS_GRAU_INSTRUCAO`** *(VARCHAR(50))*: Grau de escolaridade.
* **`CD_COR_RACA`** *(INT)* / **`DS_COR_RACA`** *(VARCHAR(30))*: Autodeclaração de cor ou raça.
* **`DT_NASCIMENTO`** *(DATE)*: Data de nascimento.
* **`CD_NACIONALIDADE`** *(INT)* / **`DS_NACIONALIDADE`** *(VARCHAR(50))*: Nacionalidade.



### 2.2. Tabelas Fato Eleitorais (TSE)

#### `FATO_CANDIDATURA`
Regista a participação efetiva de um candidato em uma determinada eleição, cargo e localidade.
* **`SQ_CANDIDATO`** *(FK, BIGINT)* ➔ `DIM_CANDIDATO.SQ_CANDIDATO`
* **`CD_MUNICIPIO_IBGE`** *(FK, VARCHAR(7))* ➔ `DIM_MUNICIPIO.CD_MUNICIPIO_IBGE`
* **`NR_PARTIDO`** *(FK, INT)* ➔ `DIM_PARTIDO.NR_PARTIDO`
* **`ANO_ELEICAO`** *(INT)*: Ano da eleição (`2018`, `2020`, `2022`, `2024`).
* **`CD_ELEICAO`** *(INT)* & **`NR_TURNO`** *(INT)*: Identificadores do pleito/turno no TSE.
* **`CD_CARGO`** *(INT)* & **`DS_CARGO`** *(VARCHAR(50))*: Cargo disputado.
* **`CD_SIT_TOT_TURNO`** *(INT)* & **`DS_SIT_TOT_TURNO`** *(VARCHAR(50))*: Resultado final (`ELEITO`, `NÃO ELEITO`, `SUPLENTE`).
* **`ST_REELEICAO`** *(CHAR(1))*: Indica se disputou reeleição (`S`/`N`).
* **`ST_DECLARAR_BENS`** *(CHAR(1))*: Indica se declarou patrimônio (`S`/`N`).

#### `FATO_FINANCEIRO_CAMPANHA`
Centraliza as métricas monetárias e arrecadações do candidato.
* **`SQ_CANDIDATO`** *(FK, BIGINT)* ➔ `DIM_CANDIDATO.SQ_CANDIDATO`
* **`ANO_ELEICAO`** *(INT)*: Ano de referência da campanha.
* **`VR_DESPESA_CONTRATADA`** *(DECIMAL(15,2))*: Total de gastos contratados.
* **`VR_GASTO_PROPAGANDA`** *(DECIMAL(15,2))*: Total gasto especificamente com publicidade/mídia.
* **`VR_RECEITA_PJ`** *(DECIMAL(15,2))*: Total de doações/recursos via Pessoas Jurídicas (quando aplicável).
* **`VR_DESPESA_MAX_CAMPANHA`** *(DECIMAL(15,2))*: Teto legal de gastos para o cargo na localidade.

#### `FATO_VOTACAO_MUNICIPIO`
Consolida as estatísticas de votação, votos de legenda e abstenção no nível municipal.
* **`CD_MUNICIPIO_IBGE`** *(FK, VARCHAR(7))* ➔ `DIM_MUNICIPIO.CD_MUNICIPIO_IBGE`
* **`ANO_ELEICAO`** *(INT)*: Ano da eleição.
* **`QT_ELEITORES`** *(INT)*: Eleitorado total apto no município.
* **`QT_VOTOS_NOMINAIS`** *(INT)*: Total de votos diretos em candidatos.
* **`QT_VOTOS_LEGENDA`** *(INT)*: Total de votos diretos nas legendas/partidos.
* **`QT_ABSTENCAO`** *(INT)*: Quantidade de eleitores ausentes.
* **`PCT_ABSTENCAO`** *(DECIMAL(5,2))*: Taxa percentual de abstenção.

#### `FATO_PROPOSTA_GOVERNO`
Mapeia os planos e propostas de governo apresentados pelos candidatos.
* **`SQ_CANDIDATO`** *(FK, BIGINT)* ➔ `DIM_CANDIDATO.SQ_CANDIDATO`
* **`ANO_ELEICAO`** *(INT)*: Ano da eleição.
* **`DS_PROPOSTA_TEXTO`** *(TEXT)*: Conteúdo do plano de governo.
* **`EIXO_TEMATICO`** *(VARCHAR(50))*: Classificação temática (`Educação`, `Saúde`, `Segurança`, etc.).

#### `FATO_BEM_CANDIDATO`
Relaciona os bens patrimoniais declarados pelos candidatos.
* **`SQ_CANDIDATO`** *(FK, BIGINT)* ➔ `DIM_CANDIDATO.SQ_CANDIDATO`
* **`NR_ORDEM_BEM_CANDIDATO`** *(INT)*: Sequencial do bem.
* **`CD_TIPO_BEM_CANDIDATO`** *(INT)* & **`DS_TIPO_BEM_CANDIDATO`** *(VARCHAR(100))*: Categoria do bem.
* **`DS_BEM_CANDIDATO`** *(TEXT)*: Detalhamento do bem.
* **`VR_BEM_CANDIDATO`** *(DECIMAL(15,2))*: Valor declarado em reais.

#### `FATO_VAGAS`
Armazena o número de cadeiras/vagas em disputa por município e cargo.
* **`CD_MUNICIPIO_IBGE`** *(FK, VARCHAR(7))* ➔ `DIM_MUNICIPIO.CD_MUNICIPIO_IBGE`
* **`ANO_ELEICAO`** *(INT)*: Ano do pleito.
* **`CD_CARGO`** *(INT)* & **`DS_CARGO`** *(VARCHAR(50))*: Cargo disputado.
* **`QT_VAGA`** *(INT)*: Número de vagas disponíveis.

#### `FATO_COLIGACAO`
Detalha a formação de coligações e federações partidárias.
* **`SQ_COLIGACAO`** *(BIGINT)*: Sequencial único da coligação no TSE.
* **`CD_MUNICIPIO_IBGE`** *(FK, VARCHAR(7))* ➔ `DIM_MUNICIPIO.CD_MUNICIPIO_IBGE`
* **`NR_PARTIDO`** *(FK, INT)* ➔ `DIM_PARTIDO.NR_PARTIDO`
* **`TP_AGREMIACAO`** *(VARCHAR(20))*: `Partido Isolado`, `Coligação` ou `Federação`.
* **`NM_COLIGACAO`** *(VARCHAR(150))*: Nome oficial da coligação.
* **`DS_COMPOSICAO_COLIGACAO`** *(TEXT)*: Siglas dos partidos integrantes.

#### `FATO_MOTIVO_CASSACAO`
Regista os fundamentos jurídicos para indeferimentos ou cassações de registros.
* **`SQ_CANDIDATO`** *(FK, BIGINT)* ➔ `DIM_CANDIDATO.SQ_CANDIDATO`
* **`NR_PROCESSO`** *(VARCHAR(50))*: Número do processo no PJe.
* **`DS_TP_MOTIVO`** *(VARCHAR(100))*: Tipo do motivo.
* **`DS_MOTIVO`** *(TEXT)*: Razão/Fundamentação jurídica.

#### `FATO_REDE_SOCIAL_CANDIDATO`
Mapeia os canais digitais declarados pelos candidatos.
* **`SQ_CANDIDATO`** *(FK, BIGINT)* ➔ `DIM_CANDIDATO.SQ_CANDIDATO`
* **`NR_ORDEM_REDE_SOCIAL`** *(INT)*: Sequência da rede.
* **`DS_URL`** *(VARCHAR(255))*: Endereço WEB do perfil/canal.



### 2.3. Tabelas Fato Socioeconômicas (IBGE & Atlas)

#### `FATO_SOCIOECONOMICO_IBGE`
Contém os dados socioeconômicos e demográficos municipais atualizados.
* **`CD_MUNICIPIO_IBGE`** *(FK, VARCHAR(7))* ➔ `DIM_MUNICIPIO.CD_MUNICIPIO_IBGE`
* **`ANO`** *(INT)*: Ano do indicador IBGE.
* **`POPULACAO`** *(INT)* & **`TIPO_POPULACAO`** *(VARCHAR(20))*: Habitações (`CENSITARIA` ou `ESTIMADA`).
* **`PIB`** *(DECIMAL(18,2))* & **`PIB_PER_CAPITA`** *(DECIMAL(12,2))*: Métricas econômicas.
* **`RENDA_DOMICILIAR_PER_CAPITA`** *(DECIMAL(10,2))*: Renda média.
* **`AREA_KM2`** *(DECIMAL(10,2))* & **`DENSIDADE_HAB_KM2`** *(DECIMAL(10,2))*: Geografia.
* **`POPULACAO_JOVEM`** *(INT)*: População em faixa etária jovem.
* **`PORCENTAGEM_SUPERIOR`** *(DECIMAL(5,2))*: % da população com ensino superior.
* **`PERFIL_MUNICIPIO`** *(VARCHAR(30))*: Perfil derivado (`Pequeno-Pobre`, `Pequeno-Rico`, `Grande-Pobre`, `Grande-Rico`).

#### `FATO_IDHM_ATLAS`
Índices de Desenvolvimento Humano Municipal do Atlas do Desenvolvimento Humano.
* **`CODMUN7`** *(FK, VARCHAR(7))* ➔ `DIM_MUNICIPIO.CD_MUNICIPIO_IBGE`
* **`ANO_REFERENCIA`** *(INT)*: Ano do Censo de referência (`1991`, `2000`, `2010`).
* **`IDHM`** *(DECIMAL(5,3))*: IDH Municipal Geral.
* **`IDHM_R`** *(DECIMAL(5,3))*: IDHM Renda.
* **`IDHM_L`** *(DECIMAL(5,3))*: IDHM Longevidade.
* **`IDHM_E`** *(DECIMAL(5,3))*: IDHM Educação.



## 3. Matriz de Relacionamentos e Mapeamento de Chaves

| Tabela Origem   | Tabela Destino               | Chave de Ligação                | Tipo de Relacionamento                                 |
| :-------------- | :--------------------------- | :------------------------------ | :----------------------------------------------------- |
| `DIM_MUNICIPIO` | `FATO_SOCIOECONOMICO_IBGE`   | `CD_MUNICIPIO_IBGE`             | 1 : N (Um município para vários anos IBGE)             |
| `DIM_MUNICIPIO` | `FATO_IDHM_ATLAS`            | `CD_MUNICIPIO_IBGE` = `CODMUN7` | 1 : N (Um município para vários anos de Censo)         |
| `DIM_MUNICIPIO` | `FATO_VOTACAO_MUNICIPIO`     | `CD_MUNICIPIO_IBGE`             | 1 : N (Um município para várias eleições)              |
| `DIM_MUNICIPIO` | `FATO_CANDIDATURA`           | `CD_MUNICIPIO_IBGE`             | 1 : N (Um município para várias candidaturas)          |
| `DIM_MUNICIPIO` | `FATO_VAGAS`                 | `CD_MUNICIPIO_IBGE`             | 1 : N (Um município para várias vagas)                 |
| `DIM_MUNICIPIO` | `FATO_COLIGACAO`             | `CD_MUNICIPIO_IBGE`             | 1 : N (Um município para várias coligações)            |
| `DIM_CANDIDATO` | `FATO_CANDIDATURA`           | `SQ_CANDIDATO`                  | 1 : N (Um candidato para várias eleições/candidaturas) |
| `DIM_CANDIDATO` | `FATO_FINANCEIRO_CAMPANHA`   | `SQ_CANDIDATO`                  | 1 : N                                                  |
| `DIM_CANDIDATO` | `FATO_PROPOSTA_GOVERNO`      | `SQ_CANDIDATO`                  | 1 : N                                                  |
| `DIM_CANDIDATO` | `FATO_BEM_CANDIDATO`         | `SQ_CANDIDATO`                  | 1 : N (Um candidato para vários bens)                  |
| `DIM_CANDIDATO` | `FATO_MOTIVO_CASSACAO`       | `SQ_CANDIDATO`                  | 1 : N                                                  |
| `DIM_CANDIDATO` | `FATO_REDE_SOCIAL_CANDIDATO` | `SQ_CANDIDATO`                  | 1 : N (Um candidato para várias redes)                 |
| `DIM_PARTIDO`   | `FATO_CANDIDATURA`           | `NR_PARTIDO`                    | 1 : N (Um partido para várias candidaturas)            |
| `DIM_PARTIDO`   | `FATO_COLIGACAO`             | `NR_PARTIDO`                    | 1 : N (Um partido em várias coligações)                |
|                 |                              |                                 |                                                        |