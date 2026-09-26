
---

## 1. Conceito e Objetivos da Normalizacao

A normalizacao de dados eh um artificio tecnico fundamental na arquitetura de sistemas, funcionando como um conjunto de regras estrategicas para garantir a organizacao logica e a eficiencia de um banco de dados relacional.

O objetivo central eh a eliminacao da reduncancias. Eh vital entender que a redundancia pode nao ser intencional, o que eh um desastre para a integridade relacional, ou aplicada deliberadamente conforme o objetivo tracado pelo negocio. O processo segue a logica da "escada": o cumprimento de um nivel de forma implica o atendimento automatico de todos os niveis inferiores. Por exemplo, se uma tabela atinge a 3 Forma normal ( 3FN ), ele ja cumpre obrigatoriamente os requisitos da 1FN e 2FN.

---

## 2. Dependencias Funcionais

As dependencias funcionais sao o alicerce para identificar anomalias e estruturar tabelas de forma eficiente. Elas definem como os atributos se relacionam entre si e coma chave.

- **Dependencia Total**: Eh o estado ideal para o 2FN, onde os atributos nao chave dependem unicamente da chave primaria em sua totalidade
- **Dependencia Parcial**: Ocorre quando um atributo depende apenas de uma parte de uma chave composta. No contexto de "remuneracoes", se o valor dependesse apenas do "professor" e ignorasse o "periodo", os dados perderiam a precisao historica e gerariam inconsistencias
- ****

---

[[Assuntos]]