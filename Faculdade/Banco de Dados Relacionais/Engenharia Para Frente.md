
# AT1 - REDUÇÃO A TABELAS

PK = chave da entidade;
FK = chave estrangeira;
Relacionamentos N:N geram tabela associativa;
### 1. Modelo 1

- BANCO (Nr PK, Nome)

- EXTRATO (Nr_Banco PK/FK, data_vencimento, diretorio)

- CONTA (id_conta PK)

- EXTRATO_CONTA (Nr_Banco, id_conta)  [PK composta]

- LANCAMENTO (Nr PK, dia, mes, descricao, tipo, valor, valor_dolar, Nr_Banco, id_conta, 
- cod_classe)

- CLASSE (cod PK, Nome)

- TAG (Cod PK, Tag)

- LANCAMENTO_TAG (Nr_Lancamento, Cod_Tag)  [PK composta]

### 2. Modelo 2
  
- BANCO (NR PK, Banco)

- CONTA (NR PK, cliente, descricao, diretorio, NR_Banco FK)

- LANCAMENTO (NR PK, Valor, Tipo, descricao, dia, mes, data_vencimento, classe, NR_Conta FK)

- TAG (cod PK, tag)

- LANCAMENTO_TAG (NR_Lancamento, cod_Tag)  [PK composta]

### 3. Modelo 3

- FUNCIONARIO (CPF PK, nome, Dept, Salario, Dt_nasc)

- DEPENDENTE (CPF PK, nome, tele)

- FUNCIONARIO_DEPENDENTE (CPF_Funcionario, CPF_Dependente, grau)  [PK composta]

### 4. Modelo 4


- CLIENTE (CPF PK, nome)

- FATURA (cod PK, descricao, valor, CPF_Cliente FK)

- PARCELAS (cod_Fatura PK/FK, num PK, valor, venc, dt_pag)

- BEBIDA (cod PK, nome, valor_unit, unid)

- ALIMENTO (cod PK, descricao, valor_unit, unid)

- FATURA_BEBIDA (cod_Fatura, cod_Bebida)  [PK composta]

- FATURA_ALIMENTO (cod_Fatura, cod_Alimento)  [PK composta]

### 5. Modelo 5

- CLIENTES (CPF PK, nome)

- VEICULOS (Placa PK, $ diaria, modelo, CPF_Cliente FK)

- SINISTROS (Cod PK, ctt, Vlr, Local)

- VEICULO_SINISTRO (Placa, Cod_Sinistro)  [PK composta]

### 6. Modelo 6



- DEPARTAMENTO (sigla PK, nome, chefe)

- CARGO (sigla PK, nome, salario_base)

- FUNCIONARIO (id PK, CPF, nome, tel, sal, horario, filiacao_pai, filiacao_mae, logradouro, nr, compl, cep, cidade, sigla_cargo FK)

- FUNCIONARIO_DEPARTAMENTO (sigla_departamento, id_funcionario)  [PK composta]

- CHEFIA (sigla_departamento, id_funcionario, data)  [PK composta]

- FUNCIONARIO_DEPENDENTE (id_funcionario PK/FK, nome PK, data, parentesco)
  

- EDIFICIO (Cod PK, dt_const, dt_vistoria)

- APARTAMENTO (Cod_Edificio PK/FK, numero PK, area)

- PESSOAS (CPF PK, nome, sexo, dt_masc)

- APARTAMENTO_PESSOA (Cod_Edificio, numero, CPF, data, tipo)  [PK composta]



#college