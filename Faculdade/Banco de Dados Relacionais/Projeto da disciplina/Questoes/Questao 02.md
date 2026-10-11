


### SQL QUERY

```SQL
WITH gastos_candidato AS (
    SELECT 
        ano_eleicao, 
        sq_candidato, 
        SUM(vr_pago) AS total_gasto
    FROM tse_teste.despesas_pagas
    GROUP BY ano_eleicao, sq_candidato
),
base_candidatos AS (
    SELECT
        c.ano_eleicao, 
        COALESCE(m.sg_uf, c.sg_ue) AS uf, 
        c.ds_cargo, 
        c.sq_candidato,
        CASE 
            WHEN c.ds_sit_tot_turno IN ('ELEITO', 'ELEITO POR QP', 'ELEITO POR MÉDIA') THEN 1 
            ELSE 0 
        END AS flag_eleito,
        g.total_gasto,
        
        MAX(g.total_gasto) OVER(PARTITION BY c.ano_eleicao, COALESCE(m.sg_uf, c.sg_ue), c.ds_cargo) AS teto_maximo_cargo_ano
        
    FROM tse_teste.candidatura c
    LEFT JOIN tse_teste.municipio m ON c.cd_municipio_tse = m.cd_municipio_tse
    INNER JOIN gastos_candidato g USING (ano_eleicao, sq_candidato)
    WHERE c.ds_cargo NOT LIKE '%VICE%' 
      AND c.ds_cargo NOT LIKE '%SUPLENTE%'
      AND c.ds_sit_tot_turno NOT IN ('INDEFERIDO', 'CASSADO', 'FALECIDO', 'CANCELADO', 'NÃO CONHECIDO', 'RENÚNCIA')
      AND c.ds_sit_tot_turno IS NOT NULL
),
faixas_gasto AS (
    SELECT 
        *,
        WIDTH_BUCKET(total_gasto, 0, teto_maximo_cargo_ano + 0.01, 4) AS faixa_financeira
    FROM base_candidatos
)
SELECT
    ano_eleicao, 
    uf,
    ds_cargo, 
    faixa_financeira,
    
    MIN(total_gasto)::numeric(14,2) AS piso_faixa_r$,
    MAX(total_gasto)::numeric(14,2) AS teto_faixa_r$,
    
    COUNT(*) AS qtd_candidatos_na_faixa,
    SUM(flag_eleito) AS qtd_eleitos,
    ROUND((SUM(flag_eleito)::numeric / COUNT(*)) * 100, 2) AS taxa_sucesso_pct,
    
    ROUND(AVG(total_gasto) FILTER (WHERE flag_eleito = 1), 2) AS media_gasto_eleitos,
    ROUND(AVG(total_gasto) FILTER (WHERE flag_eleito = 0), 2) AS media_gasto_nao_eleitos,
    
    (PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY total_gasto) FILTER (WHERE flag_eleito = 1))::numeric(14,2) AS mediana_gasto_eleitos,
    (PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY total_gasto) FILTER (WHERE flag_eleito = 0))::numeric(14,2) AS mediana_gasto_nao_eleitos

FROM faixas_gasto
GROUP BY 
    ano_eleicao,
    uf,
    ds_cargo, 
    faixa_financeira
ORDER BY 
    ano_eleicao,
    uf,
    ds_cargo, 
    faixa_financeira;
```

