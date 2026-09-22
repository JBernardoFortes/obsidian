
---

A arquitetura superescalar representa uma das inovacoes mais importantes no projeto de microprocessadores modernos, permitindo alcancar um ritmo de execucao superior a uma instrucao por ciclo de clock ( IPC > 1 ). 

---

## 1. Conceito fundamental e evolucao da arquitetura

Enquanto processadores escalares tradicionais executam no maximo uma instrucao a cada ciclo de clock ( IPC <= 1 ), a arquitetura superescalar replica componentes internos do hardware, como Unidades Logicas e Aritmeticas ( ALUs ), Unidades de Ponto Flutuante ( FPUs ) e Unidades de Load/Store. Essa multiplicacao de unidades funcionais independentes permite buscar, decodificar e despachar um bloco contendo multiplas instrucoes simultaneamente.

DIferente do superpipeline - que busca aumentar a frequencia de opereacao subdividindo os estagios do pipeline em etapas mais curtas -, a tecnica superescalar foca na emissao paralela em largura ( Multiple issue ). Isso resulta em um tempo medio por instrucao reduzido ( CPI < 1 ) e permite que a arquitetura seja aplicada tanto a processadores RISC quanto CISC.

---

## 2. O Pilar do Paralelismo em Nivel de Instrucao (ILP)




- [[Assuntos]]
- [[Questao 16 - 2025]]