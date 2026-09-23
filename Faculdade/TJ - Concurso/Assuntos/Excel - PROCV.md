
### 1. Introducao a Logica do Microsoft Excel em Provas

O Microfost Excel eh uma ferramenta de produtividade onipresente em editais de concursos publicos, sendo cobrada tanto para cargos administrativos quanto para especialistas em Tecnologia da Informacao (TI). Para dominar as questoes da prova, o candidato deve compreender a estrutura espacial da planilha:

- Colunas 
- Linhas
- Celulas

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

- [[Questao 20 - 2025]]
- [[Assuntos]]

