
---

![[AV2.AT3 Linguagem SQL Seleção básica.pdf]]

---

## Página 1

### 1. Selecione o nome do empregado (`ename`) e seu cargo (`job`);

```SQL
SELECT ename, job 
FROM emp;
```

### 2. Selecione os empregados que ganham mais que 500,00;

```SQL
SELECT * 
FROM emp 
WHERE sal > 500;
```

### 3. Selecione o nome e a data em que foi admitido (`hiredate`) dos empregados que trabalham no departamento de número 30.

```SQL
SELECT ename, hiredate 
FROM emp 
WHERE deptno = 30;
```

### 4. Quais os empregados que foram admitidos após 1° de junho de 1981?

```SQL
SELECT * 
FROM emp 
WHERE hiredate > '1981-06-01';
```

### 5. Selecione o nome e código de todos os funcionários que possuem a letra A iniciando o seu nome.

```SQL
SELECT empno, ename 
FROM emp 
WHERE ename LIKE 'A%';
```

### 6. Selecione o nome e o código de todos os funcionários que possuem a sequência AR em qualquer parte do seu nome.

```SQL
SELECT empno, ename 
FROM emp 
WHERE ename LIKE '%AR%';
```

### 7. Selecione o número do departamento, o nome e o salário dos funcionários que ganham mais de 300,00 em ordem alfabética crescente.

```SQL
SELECT deptno, ename, sal 
FROM emp 
WHERE sal > 300 
ORDER BY ename;
```

### 8. Selecione os departamentos em ordem decrescente de código.

```SQL
SELECT * 
FROM dept 
ORDER BY deptno DESC;
```

### 9. Selecione o número do departamento, o nome e o salário dos funcionários ordenados por departamento e, dentro do departamento, por salário.

```SQL
SELECT deptno, ename, sal 
FROM emp 
ORDER BY deptno, sal;
```

## Página 2

### 1. Selecione o número do departamento, o nome do funcionário e o nome do departamento dos funcionários lotados no departamento de nome 'SALES';

```SQL
SELECT emp.deptno, emp.ename, dept.dname 
FROM emp, dept 
WHERE emp.deptno = dept.deptno 
  AND dept.dname = 'SALES';
```

### 2. Refaça o exercício listando todos os departamentos e ordenando pelo nome do departamento;

```SQL
SELECT emp.deptno, emp.ename, dept.dname 
FROM emp, dept 
WHERE emp.deptno = dept.deptno 
ORDER BY dept.dname;
```

### 3. Refaça o exercício 2 retornando apenas os departamentos que possuem a letra N em seus nomes.

```SQL
SELECT emp.deptno, emp.ename, dept.dname 
FROM emp, dept 
WHERE emp.deptno = dept.deptno 
  AND dept.dname LIKE '%N%' 
ORDER BY dept.dname;
```

### 4. Mude o nome das colunas do exercício anterior para `num_dept` e `nome_dept` respectivamente.

```SQL
SELECT dept.deptno AS num_dept, dept.dname AS nome_dept 
FROM emp, dept 
WHERE emp.deptno = dept.deptno 
  AND dept.dname LIKE '%N%' 
ORDER BY dept.dname;
```

### 5. Refaça o exercício 1 colocando apelidos E e D para as tabelas EMP e DEPT respectivamente. O que muda na lista de colunas?

**O que muda:** Na lista de colunas e na cláusula `WHERE`, os prefixos com os nomes completos das tabelas (`emp.` e `dept.`) são substituídos pelos apelidos correspondentes (`E.` e `D.`).

```SQL
SELECT E.deptno, E.ename, D.dname 
FROM emp E, dept D 
WHERE E.deptno = D.deptno 
  AND D.dname = 'SALES';
```

### 6. Desafio: Selecione o nome do funcionário e o nome do seu gerente.

```SQL
SELECT E.ename AS funcionario, G.ename AS gerente 
FROM emp E, emp G 
WHERE E.mgr = G.empno;
```


---

[[Atividades]]