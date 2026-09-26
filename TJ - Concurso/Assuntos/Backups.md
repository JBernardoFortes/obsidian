
---
# Relatório de Estudos: Sistemas e Estratégias de Backup para Concursos

## 1. Conceitos Fundamentais e Importância Estratégica do Backup

No âmbito da Segurança da Informação, o backup não é uma mera tarefa acessória, mas o pilar central do **Plano de Continuidade de Negócios (BCP - Business Continuity Plan)**. Sua importância estratégica reside na garantia da resiliência organizacional frente a falhas de hardware, erros humanos, desastres naturais e, principalmente, ataques cibernéticos como o ransomware. A prática sintetiza-se na preservação da saúde da vida digital e na disponibilidade de serviços críticos, mitigando o risco de corrupção de dados.

Sob a ótica de Governança e Riscos, a dependência de uma única cópia de dados constitui um ponto único de falha (_Single Point of Failure_) inaceitável. Para que o backup cumpra seu papel na mitigação de riscos criminosos, ele deve seguir métodos estruturados que equilibrem a eficiência operacional com a eficácia da recuperação, preparando a infraestrutura para os desafios de restauração imediata.

## 2. Tipos Clássicos de Backup: Completo, Incremental e Diferencial

A escolha da estratégia de backup exige uma análise clínica da **Janela de Backup** (tempo disponível para cópia) em contraposição ao **RTO** (objetivo de tempo de recuperação).

- **Backup Completo (Full):** Realiza a cópia integral de todos os dados. É a base de qualquer estratégia. Embora garanta a restauração mais simples e rápida, exige maior tempo de execução e grande espaço de armazenamento, o que pode inviabilizar sua execução diária em grandes volumes de dados.
- **Backup Incremental:** Copia apenas os dados alterados desde o último backup (seja ele Full ou Incremental). Otimiza drasticamente a _Janela de Backup_ e o espaço em disco. **Análise "So What?":** O custo dessa agilidade na cópia é o aumento da complexidade no _restore_. A recuperação exige o último Full e _todos_ os incrementais subsequentes. Se um único link dessa cadeia falhar ou for corrompido, a integridade de toda a restauração é comprometida.
- **Backup Diferencial:** Copia os dados alterados desde o último backup _Full_. Representa um meio-termo: ocupa mais espaço que o incremental, mas simplifica a recuperação, exigindo apenas o Full e o último diferencial. Em algumas provas pode ser considerado que ele faz o backup desde o incremental ou o full.

## 3. Matriz Comparativa de Desempenho e Armazenamento

A visão holística sobre as métricas de backup permite ao gestor de TI alinhar a infraestrutura às necessidades do negócio.

|   |   |   |   |   |
|---|---|---|---|---|
|Tipo de Backup|O que é copiado|Velocidade de Cópia|Velocidade de Restore (RTO)|Espaço Consumido|
|**Full (Completo)**|Todos os dados|Mais Lenta|Mais Rápida|Máximo|
|**Incremental**|Alterações desde o último backup|Mais Rápida|Mais Lenta (Cadeia de arquivos)|Mínimo|
|**Diferencial**|Alterações desde o último Full|Intermediária|Intermediária|Médio|

**Nota Técnica:** Há uma transição tecnológica clara das fitas (LTO/DLT) para os **Storages NAS**. Enquanto as fitas operam com **acesso sequencial** (lento para localizar arquivos específicos), o NAS permite o **acesso aleatório (**_**random access**_**)**, sendo mais rápido, confiável e facilitando a gestão dinâmica dos dados.

## 4. Estratégia de Proteção: A Regra 3-2-1 e Variações Modernas

A Regra 3-2-1 é um padrão de ouro para evitar a perda total de dados em incidentes isolados:

1. **3 Cópias:** Manter o original e duas cópias adicionais.
2. **2 Mídias Diferentes:** Utilizar tecnologias distintas (ex: NAS e Nuvem) para evitar falhas simultâneas em hardwares de mesma natureza.
3. **1 Cópia Externa (Offsite):** Armazenamento em local remoto para proteção contra desastres físicos (incêndios, inundações) no site principal.

**Variação Moderna (3-2-1-0):** A evolução desta regra introduz o dígito **"0"**, que simboliza **zero erros**. Isso exige a implementação de processos automatizados de verificação de integridade e testes de consistência após cada backup. Embora a nuvem facilite a cópia _offsite_, o analista deve considerar os desafios de largura de banda e os custos de _egress_ (taxas para recuperação de dados) praticados por provedores.

## 5. Governança e Métricas de Recuperação (RPO e RTO)

A eficácia de um sistema de backup é medida pela sua capacidade de restauração dentro dos parâmetros de conformidade da organização. A periodicidade de testes de restauração (_stress tests_) é **inegociável** para o compliance do BCP.

- **RTO (Recovery Time Objective):** Tempo máximo tolerável para restabelecer um serviço após uma falha. Backups do tipo **Full** proporcionam o menor RTO.
- **RPO (Recovery Point Objective):** Define a perda de dados tolerável, medida em tempo (ex: 4 horas de dados perdidos). Determina a frequência necessária dos backups.

## 6. Segurança Aplicada e Dicas para Provas de Concursos

A proteção do backup deve abranger tanto a **Confidencialidade** quanto a **Integridade** dos dados.

- **Criptografia (Confidencialidade):**
    - **Simétrica:** Utiliza uma única chave para cifrar e decifrar. Destaca-se pela agilidade no processamento de grandes volumes.
    - **Assimétrica:** Utiliza par de chaves (pública/privada). Garante autenticidade e não-repúdio, sendo a base dos certificados digitais.
- **Hashing (Integridade):** O uso de funções de hash, como o **SHA-256**, é essencial para gerar uma "impressão digital" do backup, garantindo que os dados não foram alterados entre a origem e o destino.


---

[[Questao 36 - 2025]]
[[Assuntos]]