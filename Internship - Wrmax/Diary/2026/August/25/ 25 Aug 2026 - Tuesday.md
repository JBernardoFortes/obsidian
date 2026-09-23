- Comecei o dia tendo uma conversa com o Roberth na sala de reunioes
    - Ele disse que quer que a gente faca uma reuniao com a Vicky sobre as demandas que a gente ta desenvolvendo
    - Ele me relembrou tambem das demandas que ele me passou
        - Multipostagem
        - Integracao claude + remotion + palmier
        - O bot do wpp que capta demandas ( IN PROGRESS )
        - A integracao com o claude + gpt images + nano banana ( IN PROGRESS )
- Vou conectar o plugin que ele me passou de pegar leads e pra prospeccao do linkedkin
    - O preco eh muito caro, o Roberth disse que nao precisa bater cabeca com isso por enquanto
- A reuniao vai ser feita
    - Terminar hoje a parte de integrar o MCP com claude e gpt
        - A Vicky disse que eh tranquilo hospedar pela Vercel, se tiver env so subir la tambem
    - Depois dar uma olhada no mcp que conecta varias contas de redes sociais
- Completei o MCP com claude + gpt images
    - Tive dificuldades no deploy da aplicacao mas foi facil eventualmente
    - Me embananei com a parte de fazer deploy e definir os protocolos dentro da propria vps, os metodos de comunicacao dos container docker
    - Testei e funcionou o mcp. ele esta retornando um link para download da imagem a fim de diminuir os tokens utilizados para o claude mandar a imagem inteira
- Descobri que tem dominio na hostinger por 1 real



- Alinhei com a Victoria para fazer a parte de postagem automatica
    - A ideia inicial eh fazer algum tipo de CRON ( Um servico que roda todo dia em um horario especifico ) que ele vai checar se tem postagem marcada para o dia checando em um banco de dados PostGres do proprio n8n, tendo ele vai puxar a midia do notion e encaminhar para o fluxo de postagem, nao tendo ele so passa.
        - Gargalhos:
            - O n8n possui esse servico de CRON?
            - Como ficaria o Banco de dados?
            - Da pra puxar a midia do notion depois?
            - Garantir que a midia fique intacta ate o dia da postagem automatica



[[August]]
 