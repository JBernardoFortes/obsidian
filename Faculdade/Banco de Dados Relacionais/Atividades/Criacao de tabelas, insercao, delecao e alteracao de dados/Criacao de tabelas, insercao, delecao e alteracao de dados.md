
---

![[AV2.AT2 Linguagem SQL Criação de tabelas Inserção, Deleção e Alteração de dados.pdf]]

---

### Respostas

### 1. Crie a tabela DEPT

```SQL
CREATE TABLE DEPT (
    DEPTNO INT PRIMARY KEY,
    DNAME VARCHAR(50),
    LOC VARCHAR(50)
);
```

### 2. Crie a tabela EMP

```SQL
CREATE TABLE EMP (
    EMPNO INT PRIMARY KEY,
    ENAME VARCHAR(50),
    JOB VARCHAR(50),
    MGR INT,
    HIREDATE DATE,
    SAL DECIMAL(10,2),
    COMM DECIMAL(10,2),
    DEPTNO INT,
    FOREIGN KEY (DEPTNO) REFERENCES DEPT(DEPTNO)
);
```

### 3. Inclua pelo menos dois departamentos e tres empregados

```SQL
INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES 
(1, 'VENDAS', 'SÃO PAULO'),
(2, 'TECNOLOGIA', 'RIO DE JANEIRO');

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO) VALUES 
(101, 'CARLOS SILVA', 'ANALISTA', NULL, '2023-01-15', 3500.00, 200.00, 2),
(102, 'MARIA SOUZA', 'VENDEDORA', 101, '2023-03-10', 2500.00, 500.00, 1),
(103, 'ANA COSTA', 'GERENTE', NULL, '2022-05-20', 6000.00, NULL, 2);
```

### 4. Incluir o empregado José que trabalha no departamento 1

```SQL
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO) VALUES 
(104, 'JOSÉ', 'ASSISTENTE', 102, '2024-02-01', 2000.00, NULL, 1);
```

### 5. Alterar o nome de Jose para Paulo Jose

```SQL
UPDATE EMP 
SET ENAME = 'PAULO JOSÉ' 
WHERE ENAME = 'JOSÉ';
```

### 6. Aumentar o salario de Jose em 10%

```SQL
UPDATE EMP 
SET SAL = SAL * 1.10 
WHERE ENAME = 'PAULO JOSÉ';
```

### 7. Alterar o valor DEFAULT do salario ( `SAL` ) para 300 reais

```SQL
ALTER TABLE EMP 
ALTER SAL SET DEFAULT 300;
```

### 8. Alterar a comissao ( `COMM` ) de todos os funcionario para 5% do salario

```SQL
UPDATE EMP 
SET COMM = SAL * 0.05;
```




---
[[Atividades]]

