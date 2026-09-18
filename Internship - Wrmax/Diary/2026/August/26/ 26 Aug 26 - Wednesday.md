- Avisei ao Roberth sobre o mcp que eu subi
- Ele avisou sobre o limite do Claude, ele atribuiu a gente, mas ele foi de boa, nao foi rude.
    - Acho que foi eu que quase estourei os limites do claude, fazendo o MCP
    - Vou ficar mais esperto em como economizar tokens

### Eu ainda tenho que integrar o Nano Banana no Mcp do Claude

- Fazer um esquema onde o claude pergunta qual modelo utilizar antes de chamar o mcp.
- Vou fazer o esquema logo primeiro, depois eu vou para a parte de automatizar as postagens utilizando o n8n
    - Vou pedir ajuda do gemini dessa vez para me orientar, como nao tem claude code para n8n eu vou economizar mais tokens quando eu comecar essa task
- Parece que nao ativou o nano banana ainda, vou tentar quando o reset da week bater
- Testei a ferramenta que o Roberth me passou do Agent Reach, eh realmente viavel
- Comecei a fazer a parte de postagem automatica
    - O que eu vou fazer eh o seguinte
        - Vou criar um no trigger de 5 em 5 minutos
        - ele vai buscar no notion na coluna de posts agendados e vai filtrar pela data deles
            - O que tiver uma data de publicacao marcada para antes do horario de agora passa
        - Recuperando os posts agendados eu vou baixar midias dele, se nao houver posts eu so cancelo o fluxo.
        - Depois de baixar as midias eu puxo uma execucao do fluxo da Victoria de publicar para cada item no array e passando o que eles sao ( carrossel, reels, post )
- Amanha eu comeco a fazer a parte pratica, faltam ainda 1h mas a parte de testar eh um pouco complexa, talvez hoje eu tente fazer o webhook para puxar as postagens agendadas

#internship-wrmax 