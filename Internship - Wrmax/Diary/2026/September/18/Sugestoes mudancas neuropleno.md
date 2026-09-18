url : [neuropleno-landpage.vercel.app](https://neuropleno-landpage.vercel.app/)

atual [https://neuropleno-landpage.vercel.app/](https://neuropleno-landpage.vercel.app/)

antiga: [https://neuropleno.com.br/](https://neuropleno.com.br/)

ALTERAÇÕES 16/09

Eu mexeria nessa ordem:

- [x]   **Reescreveria completamente o primeiro bloco.** Não colocaria “Neurorradiologia” apenas como uma terceira palavra no título, porque o paciente comum nem sempre entende o que ela significa. Eu transformaria isso em benefício. Algo assim:

> **Referência em Neurologia, Neurocirurgia e Neurorradiologia em Teresina**
> 
> Do diagnóstico ao tratamento clínico, cirúrgico e endovascular de condições neurológicas complexas, com equipe especializada e tecnologia de alta precisão.
> 
> **[Agendar consulta]** **[Falar com nossa equipe]**
> 
> Neurologia • Neurocirurgia • Neurointervenção • Exames especializados

- [x] **Criaria três portas de entrada logo depois do hero.** Hoje você joga aproximadamente 20 condições/procedimentos numa mesma seção. Isso aumenta carga cognitiva. Eu colocaria três cards grandes: **Neurologia**, para AVC, Parkinson, epilepsia, demências, cefaleias etc.; **Neurocirurgia**, para tumores, coluna, trigêmeo e procedimentos cirúrgicos; e **Neurorradiologia Intervencionista**, explicando em linguagem humana: “tratamentos minimamente invasivos realizados pelos vasos sanguíneos”, com aneurisma, angioplastia de carótida, angiografia, tratamento endovascular etc. Isso posiciona a clínica como centro completo, não como “mais uma clínica de neurologia”.
	- [ ] Tirar as imagens feitas por IA e tentar arrumar outras do banco de dados deles

- [x]    **Transformaria “Referência Nacional” de slogan em prova.** Aqui está o ponto mais importante. Coloque uma seção imediatamente após o hero chamada algo como **“Por que a Neuropleno se tornou referência”**. Aí entram apenas fatos comprováveis: formação dos médicos, atuação acadêmica, tratamentos de alta complexidade, participações científicas, estrutura, número real de pacientes, anos de atuação, publicações e presença na imprensa. A página já mostra médicos com CRM/RQE e qualificações relevantes; isso é muito mais poderoso do que repetir “tecnologia de ponta”.

 - [x] **Pelo amor de Deus, arrume a prova de mídia.** Hoje aparece “Já falamos sobre saúde neurológica em” com Terra, Globo, iG, UOL, Valor e O Globo. Mas, na estrutura que consegui inspecionar, os itens levam aos próprios arquivos das logos, não às reportagens. Isso enfraquece uma prova que poderia ser fortíssima. Faça cada logo abrir a matéria real. Melhor ainda: mostre **logo + manchete + assunto + “Ler reportagem”**. Se você quer sustentar “Referência Nacional”, isso é ouro.
	 - Tem um problema que eu nao achei as reportagens nos demais canais alem do Terra

- [x] **Eu mudaria “Agendar Avaliação” para “Agendar Consulta”.** “Avaliação” tem uma linguagem muito de funil/comercial. Para medicina, “Agendar consulta” passa mais naturalidade e confiança. Como CTA secundário, use **“Falar com a equipe pelo WhatsApp”**. E o botão precisa abrir mensagem contextualizada. Se a pessoa veio de aneurisma, não deveria chegar no WhatsApp dizendo apenas “Olá”. O atendimento já deveria saber de onde veio. Só tenha cuidado para não enviar dados de saúde pessoais para pixels e plataformas de publicidade; isso precisa ser tratado com atenção em LGPD e nas regras das plataformas.

- [x] **Eu colocaria a equipe muito mais cedo.** Hoje a equipe aparece relativamente tarde, depois de sintomas, procedimentos, exame, “como funciona” e diferenciais. Em saúde de alta complexidade, o paciente compra confiança no médico antes de comprar tecnologia. Eu colocaria pelo menos uma faixa logo após a prova de autoridade: fotos reais dos quatro médicos + especialidade + RQE + principal área de atuação. Depois, mais abaixo, a versão completa.

- [ ] **Revisaria algumas promessas médicas.** Na seção de eletroneuromiografia, a página afirma que o exame é “sem dor, rápido”. Eu retiraria “sem dor”. A EMG pode envolver eletrodos de agulha e causar desconforto ou dor transitória, dependendo do paciente e da etapa do exame. Use algo como: **“Exame realizado com cuidado, orientação em todas as etapas e por equipe especializada em neurofisiologia.”** É mais seguro e mais crível.

**8 Há um problema de SEO local e de consistência cadastral que eu verificaria imediatamente.** A landing mostra o endereço na **R. Gov. Joca Pires, 2020**, enquanto o cadastro do CNES que encontrei ainda apresenta **Rua Governador Artur de Vasconcelos, 289**, apesar de indicar atualização em 2026. Pode haver explicação — mudança de sede, unidade distinta etc. — mas Google Business Profile, CNES, CRM, site, Maps e diretórios precisam conversar entre si. Inconsistência de NAP prejudica SEO local e também confiança.

**9 Tecnicamente, eu não deixaria essa landing em `vercel.app` quando entrar em produção.** O domínio principal já existe. Eu colocaria algo como `neuropleno.com.br` ou uma rota do próprio domínio, configuraria canonical, Search Console, sitemap, schema de `MedicalClinic`/`Physician`, dados estruturados dos médicos, Open Graph, GA4 e acompanhamento de conversões. E criaria páginas próprias para **Neurologia em Teresina**, **Neurocirurgia em Teresina**, **Neurorradiologia em Teresina**, **Aneurisma cerebral**, **AVC**, **Eletroneuromiografia** etc. Essa landing pode vender; essas páginas específicas é que vão construir autoridade orgânica.

Também colocaria no footer os dados institucionais exigidos pela publicidade médica. Hoje consigo ver CRM/RQE nos cards dos médicos, mas não encontrei no rodapé da landing a identificação do **registro da clínica no CRM e do diretor técnico-médico**, que a Resolução CFM nº 2.336/2023 exige para publicidade de estabelecimentos assistenciais em ambiente virtual. Confirmem com a clínica quais são os dados corretos antes de publicar.

A estrutura que eu montaria seria, no fundo, esta: **autoridade → prova → escolha da especialidade → condições tratadas → médicos → procedimentos de alta complexidade → estrutura → mídia → como funciona → FAQ → CTA**. Hoje a página está mais próxima de **sintomas → catálogo → explicação → equipe**. Essa inversão muda a percepção da Neuropleno de clínica generalista para **centro de referência neurológica de alta complexidade**.

E tem uma chave aqui: **Neurorradiologia não deve ser só adicionada ao texto. Ela precisa mudar a narrativa do site.** É ela que permite comunicar que vocês não ficam apenas em consulta e cirurgia: existe diagnóstico vascular e tratamento endovascular dentro do ecossistema neurológico. No fundo, é isso que diferencia.

Se eu estivesse desenvolvendo essa landing, minha próxima versão começaria o hero assim:

> **Referência Nacional em Neurologia, Neurocirurgia e Neurorradiologia**
> 
> **Cuidado neurológico completo, do diagnóstico ao tratamento de alta complexidade, em Teresina.**
> 
> Consultas, exames especializados, cirurgia e tratamentos endovasculares conduzidos por uma equipe médica multidisciplinar.
> 
> **Agendar consulta pelo WhatsApp**

E logo abaixo: **“Conheça as três áreas de atuação”** com os três cards. Isso já muda completamente o posicionamento.


Tirar o "aqui" de Teresina tambem