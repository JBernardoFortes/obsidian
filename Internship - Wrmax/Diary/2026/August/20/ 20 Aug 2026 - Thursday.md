- Hoje eu vou tentar rodar localmente a automacao de gerar tasks automaticas utilizando o OpenWA + Claude + NodeJs / n8n
    
- Decidi fazer em NodeJs mesmo o projeto, para me ater mais a ele e me dar um animo para fazer e aprender, alem de nao abandonar a parte de codigo que eh o que eu realmente me interesso.
    
- Comecei a estruturar o projeto utilizando Node + Express + Postgress
    
- O claude me gerou um markdown dos objetivos do sprint de hoje:
    

    
- Hoje consegui terminar o planejado com bastante tempo de folga, implementei o webhook que recebe as mensagens do numero as registra em um banco de dados
    
    - Ela registra apenas os clientes filtrados, pre-cadastrados do banco
    - a parte de lote ainda nao foi implementada, tendo em vista que precisa utilizar node-cron, uma complexidade a mais
    - proximo passo eh justamente criar esse job com cron para verificar e formar os lotes
- Eu complementei tudo e sobrou 2h30min de tempo ainda de expediente, vou adiantar algumas coisas como o node-cron para gerar os lotes de mensagens
    
- Pedi para o claude me gerar esse planejamento do debounce
    
    
    
- Finalizei as tasks do dia:
    
    - Fiz a captacao de mensagens com os numeros filtrados
        - Ele so guarda no banco de dados as mensagens dos numeros que estao filtrados
    - Fiz o debounce do webhook
        - Ele espera 4 minutos desde o comeco da primeira mensagem para criar o lote
        - ou
        - Ele aguarda 1 minuto de silencio entre as mensagens para criar o lote
        - Essas configuracoes foram feitas em dev, em producao os valores sao outros
- Para o dia de amanha vou comecar a fazer a classificacao das mensagens em demandas ou nao, e comecar a criar um contexto para o modelo se basear
    
- ## Pedi para o Claude me gerar um planejamento para o dia de amanha


[[August]]