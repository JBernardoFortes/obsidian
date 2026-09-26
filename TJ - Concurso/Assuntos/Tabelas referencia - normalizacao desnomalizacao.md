---

---


---

# Formas Normais — Banco de Dados

## 1. Tabela Não Normalizada (UNF — Unnormalized Form)

Apresenta **grupos repetitivos** (múltiplos telefones e idiomas na mesma célula) e atributos compostos.

|ID_Aluno|Nome|Curso|Idiomas|Telefones|Cidade|CEP|
|---|---|---|---|---|---|---|
|**1**|João|Matemática|Inglês, Espanhol|9999-1111, 9999-2222|São Paulo|01000-000|
|**2**|Maria|Física|Francês|8888-3333|Rio de Janeiro|22000-000|

---

## 2. Primeira Forma Normal (1FN)

Garante a **atomicidade**, ou seja, cada célula contém apenas um valor indivisível, eliminando listas e grupos repetitivos.

|ID_Aluno|Nome|Curso|Idioma|Telefone|Cidade|CEP|
|---|---|---|---|---|---|---|
|**1**|João|Matemática|Inglês|9999-1111|São Paulo|01000-000|
|**1**|João|Matemática|Inglês|9999-2222|São Paulo|01000-000|
|**1**|João|Matemática|Espanhol|9999-1111|São Paulo|01000-000|
|**1**|João|Matemática|Espanhol|9999-2222|São Paulo|01000-000|
|**2**|Maria|Física|Francês|8888-3333|Rio de Janeiro|22000-000|

---

## 3. Segunda Forma Normal (2FN)

Elimina **dependências parciais**, ou seja, atributos não-chave que dependem de apenas parte de uma chave primária composta.

### Exemplo A: Separação de Alunos, Telefones e Idiomas

#### Tabela: Alunos

|ID_Aluno (PK)|Nome|ID_Cidade (FK)|
|---|---|---|
|**1**|João|10|
|**2**|Maria|20|

#### Tabela: Telefones

|ID_Telefone (PK)|ID_Aluno (FK)|Telefone|
|---|---|---|
|**1**|1|9999-1111|
|**2**|1|9999-2222|
|**3**|2|8888-3333|

#### Tabela: Idiomas

|ID_Aluno (FK)|Idioma|
|---|---|
|**1**|Inglês|
|**1**|Espanhol|
|**2**|Francês|

### Exemplo B: Professores e Remunerações por Período

#### Tabela: Professores

|ID_Professor (PK)|Nome_Professor|ID_Cidade (FK)|
|---|---|---|
|**101**|Carlos|1|
|**102**|Ana|2|

#### Tabela: Remunerações

|ID_Professor (FK)|Período|Valor_Remuneração|
|---|---|---|
|**101**|2026-01|R$ 5.000,00|
|**101**|2026-02|R$ 5.500,00|
|**102**|2026-01|R$ 6.000,00|

---

## 4. Terceira Forma Normal (3FN)

Elimina **dependências transitivas**, ou seja, atributos não-chave que dependem de outros atributos não-chave.

Também evita o armazenamento de **campos calculados ou derivados** quando eles podem ser obtidos a partir de outros dados.

### Tabela: Cidades

|ID_Cidade (PK)|Nome_Cidade|CEP|
|---|---|---|
|**10**|São Paulo|01000-000|
|**20**|Rio de Janeiro|22000-000|

### Tabela: Alunos

Sem o campo calculado `Idade`.

|ID_Aluno (PK)|Nome|Data_Nascimento|
|---|---|---|
|**1**|João|2000-05-15|
|**2**|Maria|1998-10-20|

---

## 5. Forma Normal de Boyce-Codd (FNBC)

Garante que **todo determinante de uma dependência funcional seja uma superchave**.

### Tabela: Disciplinas e Professores

|ID_Professor (PK/FK)|Disciplina|
|---|---|
|**101**|Matemática|
|**102**|Física|

### Tabela: Disciplinas e Salas

|Disciplina (PK)|Sala|
|---|---|
|**Matemática**|A101|
|**Física**|A102|

### Tabela: Aulas

|ID_Aula (PK)|ID_Professor (FK)|ID_Disciplina (FK)|
|---|---|---|
|**1**|101|MAT-01|
|**2**|102|FIS-01|

---

## 6. Quarta e Quinta Formas Normais (4FN e 5FN)

Isolam **dependências multivaloradas independentes** (4FN) e **dependências de junção** (5FN).

### Tabela: Cursos

|ID_Aluno (FK)|Curso|
|---|---|
|**1**|Matemática|
|**2**|Física|

### Tabela: Anos de Ingresso de Professores

|ID_Ano (PK)|Ano_Ingresso|
|---|---|
|**2010**|2010|
|**2015**|2015|

### Tabela: Lotação de Professores

|ID_Professor (PK)|Nome_Professor|ID_Cidade (FK)|ID_Ano (FK)|
|---|---|---|---|
|**101**|Carlos|1|2010|
|**102**|Ana|2|2015|

---

## 7. Tabela Desnormalizada

### Visão Consolidada para OLAP / Data Warehouse

Reúne intencionalmente as tabelas em uma única estrutura para evitar **JOINs** custosos e otimizar a velocidade de leitura em consultas analíticas.

|ID_Aluno|Nome|Data_Nascimento|Nome_Cidade|CEP|Curso|Idioma|Telefone|
|---|---|---|---|---|---|---|---|
|**1**|João|2000-05-15|São Paulo|01000-000|Matemática|Inglês|9999-1111|
|**1**|João|2000-05-15|São Paulo|01000-000|Matemática|Espanhol|9999-2222|
|**2**|Maria|1998-10-20|Rio de Janeiro|22000-000|Física|Francês|8888-3333|

---

## Resumo

|Forma Normal|Objetivo principal|
|---|---|
|**UNF**|Estrutura não normalizada, com grupos repetitivos|
|**1FN**|Garantir atomicidade dos valores|
|**2FN**|Eliminar dependências parciais|
|**3FN**|Eliminar dependências transitivas|
|**FNBC**|Todo determinante deve ser uma superchave|
|**4FN**|Eliminar dependências multivaloradas|
|**5FN**|Eliminar dependências de junção|
|**Desnormalização**|Otimizar consultas analíticas, aceitando redundância|