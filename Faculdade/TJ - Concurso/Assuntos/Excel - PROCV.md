
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

#### Limitacoes e Pulo do gato

Nativamente, o PROCV so pesquisa para a direita. O criterio de busca deve estar obrigatoriamente na coluna 1 da matriz. Para realizar uma busca para a esquerda, utiliza-se funcao ESCOLHER como um artificio tecnico

- **Logica**: Atraves de uma constante de matriz como {1/2} ou {2/1}, eh possivel reordenar virtualmente as colunas
- **Exemplo**: 

```excel
=PROCV(F2, ESCOLHER({2/1}); A2:A17; C2:C17); 2; 0)
```

	Aqui, o Excel engana a funcao, invertendo a ordem das colunas A e C para permitir a busca.


### 3. Guia de Diagnostico: Tratamento de Erros no PROCV



---

### 4. Operadores Fundamentais de Intervalo

Nao confunda os operadores, pois esta eh uma pegadinha classica:

- **Dois-pontos ( : )**: Significa "Ate". Define um intervalo continuo ( ex: `A1:A10` engloba todas as 10 celulas)
- **Ponto e virgula ( ; )**: Significa "e". Define uma uniao de celulas isoladas ou separa argumentos (ex: `SOMA(A1;A10)` soma apena as duas celulas)


---

### 5. Analise de Funcoes Estatisticas e Condicionais

#### Operacoes basicas e estatisticas:

- **SOMA, MINIMO e MAXIMO**: Aplicacoes diretas de adicao e identificacao de extremos absolutos.
- 


---

- [[Questao 20 - 2025]]
- [[Assuntos]]

