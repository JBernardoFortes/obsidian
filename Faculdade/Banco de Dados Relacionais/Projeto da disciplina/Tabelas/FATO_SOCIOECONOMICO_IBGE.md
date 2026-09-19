# Dicionário de Dados - Tabela FATO_SOCIOECONOMICO_IBGE

Armazena indicadores demográficos, econômicos e educacionais consolidados pelo IBGE a nível municipal.



##  Dicionário dos Campos

| Variável | Tipo | Descrição | Domínio / Valores Possíveis |
| :--- | :--- | :--- | :--- |
| **CD_MUNICIPIO_IBGE** | Texto | Código IBGE do município (Chave Estrangeira). | Código IBGE de 7 dígitos |
| **ANO** | Numérico | Ano de referência do indicador socioeconômico. | AAAA |
| **POPULACAO** | Numérico | População residente do município. | Número de habitantes |
| **TIPO_POPULACAO** | Texto | Natureza da apuração populacional. | `CENSITARIA`, `ESTIMADA` |
| **PIB** | Decimal | Produto Interno Bruto municipal a preços correntes. | Valor monetário em R$ |
| **PIB_PER_CAPITA** | Decimal | PIB per capita oficial do município. | R$ por habitante |
| **RENDA_DOMICILIAR_PER_CAPITA** | Decimal | Rendimento médio domiciliar per capita no município. | Valor monetário em R$ |
| **AREA_KM2** | Decimal | Área territorial do município em km². | Valor em km² |
| **DENSIDADE_HAB_KM2** | Decimal | Relação entre população residente e área territorial. | habitantes/km² |
| **POPULACAO_JOVEM** | Numérico | População em faixas etárias jovens (ex: 16-29 anos). | Número de habitantes |
| **PORCENTAGEM_ANALFABETISMO** | Decimal | Percentual da população não alfabetizada. | `0` a `100%` |
| **PORCENTAGEM_SUPERIOR** | Decimal | Percentual da população com ensino superior completo. | `0` a `100%` |
| **PERFIL_MUNICIPIO** | Texto | Classificação de perfil (faixa populacional x riqueza). | `Pequeno-Pobre`, `Pequeno-Rico`, `Grande-Pobre`, `Grande-Rico` |
[[Tabelas]]