
### 1. Introducao a Logica do Microsoft Excel em Provas

O Microfost Excel eh uma ferramenta de produtividade onipresente em editais de concursos publicos, sendo cobrada tanto para cargos administrativos quanto para especialistas em Tecnologia da Informacao (TI). Para dominar as questoes da prova, o candidato deve compreender a estrutura espacial da planilha:

- **Colunas**: Sao estruturas verticais ( dispostas de cima para baixo), identificadas por letras ( A, B, C... ) no cabecalho horizontal
- **Linhas**: Sao estruturas horizontais ( dispostas da esquerda para a direita ), identificadas por numeros ( 1,2,3... ) na barra lateral vertical
- **Celulas**: O ponto de intersecao entre uma coluna e uma linha (ex: `B5`)

---

### 2. A Funcao PROCV ( Pesquisa Vertical )

A funcao PROCV ( VLOOKUP ) eh uma ferramenta de pesquisa e referencia que realiza uma busca vertical na coluna mais a esquerda de um intervalo selecionado. Ao encontrar o valor, ela retorna o dado presente em uma coluna especifica da mesma linha.

A sintaxe oficial eh: ``````
```excel
=PROCV(valor_procurado; matriz_tabela; num_indice_coluna;[procurar_intervalo])
```

1. Valor procurado: O item a ser localizado na primeira coluna da matriz. Se for texto, deve estar entre aspas.
2. matriz_tabela: O intervalo total de dados ( ex: A1:D50 ). A busca ocorre na primeira coluna deste intervalo
3. num_indice_coluna: O numero da coluna de onde o valor de retorno sera extraido comecando em 1 para a coluna mais a esquerda do intervalo
4. procurar_intervalo ( Logica binaria ): Define a precisao da busca
	- 0 ou FALSO: Correspondencia exata
	- 1 ou VERDADEIRO: Correspondencia aproximada(exite que a primeira coluna esteja classificada em ordem ascendente)


#### Se esse quarto elemento for omitido, o Excel assume por padrao o valor 1/VERDADEIRO.

#### Limitacoes e Pulo do gato

Nativamente, o PROCV so pesquisa para a direita. O criterio de busca deve estar obrigatoriamente na coluna 1 da matriz. Para realizar uma busca para a esquerda, utiliza-se funcao ESCOLHER como um artificio tecnico

- **Logica**: Atraves de uma constante de matriz como {1/2} ou {2/1}, eh possivel reordenar virtualmente as colunas
- **Exemplo**: 

```excel
=PROCV(F2, ESCOLHER({2/1}); A2:A17; C2:C17); 2; 0)
```

	Aqui, o Excel engana a funcao, invertendo a ordem das colunas A e C para permitir a busca.


### 3. Guia de Diagnostico: Tratamento de Erros no PROCV



| Erro        | Causa Provavel                                                                                                     | Solucao Baseada na Fonte                                                |
| ----------- | ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| \#N/D       | Valor nao encontrado (FALSO) ou, se VERDADEIRO, o `valor_procurado` eh menor que o menor valor da primeira coluna. | Verificar a existencia do valor ou classificar se usar busca aproximada |
| \#REF!      | O `num_indice_coluna` eh maior que a quantidade de colunas na matriz                                               | Ajustar o indice para um numero dentro dos limites do intervalo         |
| \#VALOR!    | O `num_indice_coluna` eh menor que 1                                                                               | Corrigir o indice para um numero inteiro igual ou superior a 1          |
| \#NOME?     | Erro de digitacao no nome da funcao ou falta de aspas em criterio de texto                                         | Corrigir ortografia da funcao ou inserir as aspas obrigatorias          |
| \#DESPEJAR! | Conflito de intersecao implicita (uso de coluna inteira como A:A em vez de uma celula unica como A2).              | Ancorar a referencia com @( ex: @A:A ) ou usar referencias de celulas   |



---

### 4. Operadores Fundamentais de Intervalo

Nao confunda os operadores, pois esta eh uma pegadinha classica:

- **Dois-pontos ( : )**: Significa "Ate". Define um intervalo continuo ( ex: `A1:A10` engloba todas as 10 celulas)
- **Ponto e virgula ( ; )**: Significa "e". Define uma uniao de celulas isoladas ou separa argumentos (ex: `SOMA(A1;A10)` soma apena as duas celulas)


---

### 5. Analise de Funcoes Estatisticas e Condicionais

#### Operacoes basicas e estatisticas:

- **SOMA, MINIMO e MAXIMO**: Aplicacoes diretas de adicao e identificacao de extremos absolutos.
- **MEDIA vs MED**: A **MEDIA** eh a media aritmetica simples. A funcao **MED**( mediana ) identifica o valor central
- **MAIOR vs. MAXIMO e MENOR vs. MINIMO**: Enquanto o MAXIMO/MINIMO sao absolutos, **MAIOR** e **MENOR** exigem um argumento 'k' ( posicao no ranking ). Ex: `=MAIOR(A1:A10; 2)` para o segundo maior. Se "k" for invalido ou maior que o numero de dados, ocorrera erro.

#### Funcoes Logicas e de Contagem

- **SE**: Estrutura `(teste_logico; valor_se_verdadeiro; valor_se_falso)`. Admite o "aninhamento" ( Uma funcao SE dentro de outra) para multiplos criterios.
- **SOMASE** e **CONT.SE**: Conta celulas que nao estao vazias, independentemente de conterem numeros, textos ou erros.
- **CONT.VALORES**: Conta celulas que nao estao vazias, independentemente de conterem numeros, textos ou erros.

---

### 6. A Evolucao: PROCX (XLOOKUP)

O PROCX eh o sucessor moderno do PROCV ( disponibvel no Microsoft 365 ). Suas vantagens principais sao:

1. **Direcao independente**: Busca em qualquer direcao ( resolve a limitacao da esquerda)
2. **Exatidao Nativa**: Por padrao, a busca eh exata ( nao precisa do "0" ou "FALSO")
3. **Flexibilidade**: Nao exige a contagem de indices de coluna, reduzindo erros de referencia

--- 

### 7. Conclusao e Dicas para o Candidato

Para gabaritar Excel, foque na sintaxe:

- **Aspas Duplas**: Obrigatorias para textos em formulas ( ex: `"Aprovado"`)
- **Curingas e Escape**: O asterisco ( `*` ) reprsenta varios caracteres; a interrogacao (`?`)  representa um unico caractere. Se a questao pedir para localizar o simbolo reall de asterisco ou interrogacao, deve-se usar o til(~) antes deles ( Ex: `"~*"` para achar um asterisco literal).
- **Referencias Absolutas**: Utilize o cifrao (`$`) para travar celulas (ex: `$A$1`) e evitar que o intervalo mude ao arrastar a formula
- **Limpeza**: Lembre-se das funcoes **ARRUMAR** ou **LIMPAR** para remover espacos extras que invalidam buscas.

---

- [[Questao 20 - 2025]]
- [[Assuntos]]

