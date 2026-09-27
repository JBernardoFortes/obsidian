
---

[[Tabelas referencia - normalizacao desnomalizacao]]

--- 
## 1. Conceito e Objetivos da Normalizacao

A normalizacao de dados eh um artificio tecnico fundamental na arquitetura de sistemas, funcionando como um conjunto de regras estrategicas para garantir a organizacao logica e a eficiencia de um banco de dados relacional.

O objetivo central eh a eliminacao da reduncancias. Eh vital entender que a redundancia pode nao ser intencional, o que eh um desastre para a integridade relacional, ou aplicada deliberadamente conforme o objetivo tracado pelo negocio. O processo segue a logica da "escada": o cumprimento de um nivel de forma implica o atendimento automatico de todos os niveis inferiores. Por exemplo, se uma tabela atinge a 3 Forma normal ( 3FN ), ele ja cumpre obrigatoriamente os requisitos da 1FN e 2FN.

---

## 2. Dependencias Funcionais

As dependencias funcionais sao o alicerce para identificar anomalias e estruturar tabelas de forma eficiente. Elas definem como os atributos se relacionam entre si e coma chave.

- **Dependencia Total**: Eh o estado ideal para o 2FN, onde os atributos nao chave dependem unicamente da chave primaria em sua totalidade
- **Dependencia Parcial**: Ocorre quando um atributo depende apenas de uma parte de uma chave composta. No contexto de "remuneracoes", se o valor dependesse apenas do "professor" e ignorasse o "periodo", os dados perderiam a precisao historica e gerariam inconsistencias
- **Dependencia Transitivo** Acontece quando um atributo nao chave depende de outro atributo que tambem nao eh chave. Um exemplo classico: Em uma tabela de aluon, a "idade" depende da "data de nascimento", que por sua vez depende do ID do aluno. Manter a idade viola a integridade, pois ela deve ser calculada dinamicamente, nao armazenada.

Uma vez compreendida as dependencias, aplicamos as regras sequenciais das Formas Nominais.

---

## 3. Detalhamento das Formas Nominais ( 1FN a 5FN e FNBC )

1. **1FN**: Exige **Atomicidade**. Atributos devem ser indivisiveis, proibindo campos multivalorados. Conforme a Tabela 1 da fonte, isso significa que cada professor possui apenas um nome ( sem homonimos ) e cada localidade ( cidade ) aparece de ofrma unica e atomica
2. **2FN**: Focada na **eliminacao de dependencias parciais**. A tabela ja deve estar na 1FN e todos os atributos nao chave devem depender da chave primaria completa
3. **3FN**: Foca na **eliminacao de dependencias transitivas**. Atributos nao chave devem ser independentes entre si, dependendo apenas da chave primaria
4. **FNBC ( Forma Normal de Boyce-Codd )**: Um refin amento da 3FN onde **Todo atributo nao chave precisa depender funcionalmente diretamente da chave**, seja ela primaria ou candidata. Isso garante a independencia absoluta de atributos nao chave, isolando dados de professores e disciplinas em tabelas proprias ( Tabelas 5,6 e 7) para evitar problemas nas dependencias
5. **4FN**: Proibe **Dependencias multivaloradas**. Atributos que contem multiplos valores que se repetem para diversos registros devem ser isolados em **subconjuntos menores**. A fonte exemplifica a decomposicao da tabela principal de professores em novas tabelas de "Cidades" e "Anos de Ingreso" ( Tabelas 8, 9 e 10 ), que sao entao referenciados 
6. **5FN**: Trata de **dependencia de juncao**. A tabela deve poder ser decomposta em subtabelas de modo que a reconstrucao da informacao original seja garantida. O foco aqui eh a capacidade de identificar cada campo em suas **tabelas de origem** apos a juncao ( Tabelas 11, 12 e 13).

Embora a normalizacao busque a perfeicao, cenarios de alta performance exigem o caminho inverso

---

## 4. Desnormalizacao de Banco de Dados

A desnormalizacao eh o uso estrategico de **redundancia intencional**. O design de um banco eh um equilibrio entre a pureza teorica e a necessidade pratica: a redundancia eh permitida **|dependendo do objetivo a ser tracado"**.

Os "trade-offs" sao claros:sacrifica-se economia de espaco e facilidade de atualizacao em favor da **agilidade de consulta**. Niveis baixos na escala de normalizacao sao usados quando o desempenho de leitura eh a prioridade absoluta. Isso eh sintetizada em ambientes analiticos ( **OLAP** ), onde a repeticao de dados facilita a extracao de grandes volumes de informacao sem o custo de multiplas juncoes complexas

---

## 5. Tabela Comparativa das Formas Normais


| Forma Normal | Regra Principal                          | Conceito-chave                       |
| ------------ | ---------------------------------------- | ------------------------------------ |
| 1FN          | Atributos atomicos e indivisiveis        | Atomicidade                          |
| 2FN          | Sem dependencia parcial                  | Chave Primaria Completa              |
| 3FN          | Sem dependencia transitiva               | Independencia entre nao chaves       |
| FNBC         | Todo determinante deve ser <br>uma chave | Independencia de atributos nao chave |
| 4FN          | Sem dependencias multivaloradas          | Subconjuntos                         |
| 5FN          | Sem dependencia de juncao                | Tbelas de Origem                     |


---

[[Assuntos]]
[[Questao 46 - 2025]]