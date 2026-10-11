


### SQL QUERY

```sql
WITH historico AS (
SELECT
c.ano_eleicao,
c.sq_candidato,
ca.nm_candidato,
c.sg_partido AS partido,
c.ds_cargo AS cargo,
c.sg_ue AS uf,
c.cd_municipio_tse AS municipio,
c.nr_turno_resultado AS turno,
c.ds_sit_tot_turno AS situacao,
c.qt_votos_totais AS votos,

COALESCE(r.total_receitas, 0) AS total_receitas,
COALESCE(r.receitas_detalhadas, '[]'::jsonb) AS receitas,
COALESCE(d.total_despesas, 0) AS total_despesas,
COALESCE(d.despesas_detalhadas, '[]'::jsonb) AS despesas,
COALESCE(b.total_bens, 0) AS patrimonio_declarado,
COALESCE(b.bens_detalhados, '[]'::jsonb) AS bens

FROM tse_teste.candidatura c

JOIN tse_teste.candidato ca

ON ca.id_pessoa_projeto = c.id_pessoa_projeto

LEFT JOIN (

SELECT
ano_eleicao,
sq_candidato,
SUM(vr_receita) AS total_receitas,
OALESCE(b.total_bens, 0) AS patrimonio_declarado,
jsonb_agg(
jsonb_build_object(
'fonte', ds_fonte_receita,
'origem', tp_origem_recurso,
'valor', vr_receita
)

ORDER BY vr_receita DESC
) AS receitas_detalhadas
FROM tse_teste.receitas_campanha

GROUP BY
ano_eleicao,
sq_candidato
) r

ON r.ano_eleicao = c.ano_eleicao

AND r.sq_candidato = c.sq_candidato

LEFT JOIN (

SELECT
ano_eleicao,
sq_candidato,
SUM(vr_pago) AS total_despesas,
jsonb_agg(
jsonb_build_object(
'despesa', ds_despesa,
'categoria', ds_categoria_despesa,
'valor', vr_pago
)


ORDER BY vr_pago DESC
) AS despesas_detalhadas

FROM tse_teste.despesas_pagas

GROUP BY
ano_eleicao,
sq_candidato
) d

ON d.ano_eleicao = c.ano_eleicao

AND d.sq_candidato = c.sq_candidato

LEFT JOIN (

SELECT
ano_eleicao,
sq_candidato,
SUM(vr_bem) AS total_bens,
jsonb_agg(
jsonb_build_object(
'tipo', ds_tipo_bem,
'descricao', ds_bem,
'valor', vr_bem
)

ORDER BY vr_bem DESC
) AS bens_detalhados

FROM tse_teste.bens_declarados

GROUP BY
ano_eleicao,
sq_candidato
) b

ON b.ano_eleicao = c.ano_eleicao

AND b.sq_candidato = c.sq_candidato

WHERE c.id_pessoa_projeto = 1009
)

SELECT *

FROM historico

ORDER BY ano_eleicao;
```