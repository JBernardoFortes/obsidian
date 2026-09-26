---

---

---

[[2nd Lista]]

---

### 1. Explique as duas iniciativas que normalmente resolver o problema de lock-in de dados em computacao em nuvem

1. Padronizar as APIs

	A ideia eh que os diferentes provedores de nuvem utilizem padroes e interfaces comuns. Dessa forma, uma aplicacao desenvolvida para um provedor poderia ser transferida para outro com menor esforco.

	- DMTF: Padronizacao de interacoes entre ambientes de nuvem
	- OCCI-WG: Desenvolvimento de uma API para o gerenciamento de servicos de nuvem
	- IEEE P2301: Portabilidade
	- IEEE P2302: Interoperabilidade entre nuvens

2. Abordagens baseadas em modelos ( Model-Driven Engineering - MDE )

	A segunda iniciativa consiste em utilizar engenharia orientada a modelos para desenvolver as aplicacoes em um nivel mais abstrato e independente da plataforma.

	A aplicacao seria inicialmente representada por modelos independentes do provedor e esses modelos poderiam ser transformados automaticamente para uma plataforma especifica. Isso reduz a necessidade de reconstruir todo o sistema quando ocorre uma mudanca no provedor.

### 2. Quais foram as duas solucoes identificadas para migrar sistemas legados para um ambiente de computacao em nuvem?

1. Reengenharia completa do sistema

	Consiste em reconstrui o software para uma nova plataforma, adaptando-o as tecnologias e caracteristicas da computacao em nuvem.

	O problema eh que uma reengenharia completa normalmente possui custo elevado, principalmente quando o sistema legado ainda eh essencial para a organizacao

2. Migrar o sistema legado sem realizar uma reengenharia completa

	A segunda alternativa eh migrar o software legado diretamente para uma infraestrutura de nuvem, procurando garantir seu funcionamento no novo ambiente sem reconstruir completamente o sistema.

	Essa alternativa evita parte do custo de uma reconstrucao completa. entretanto, o paper aponta que ainda era necessaria uma estrategia mais formal, com um processo passo a passo para realizar esse tipo de migracao considerando os diferentes servicos disponiveis na nuvem.

### 3. Liste e descreva cinco possibilidades de implementacao em MaaS

1. Modelagem colaborativa e distribuida

	Criar ferramentas que permitam que diferentes membros de uma equipe, mesmo estando distribuidos, possam especificar, compartilhar e trabalhar colaborativamente sobre modelos de software utilizando a nuvem.

2. Modeling mash-ups

	Combinar servicos de MDE provenientes de diferentes fornecedores, formando uma composicao de servicos de modelagem.

3. Mecanismos de transformacao de modelos na nuvem

	Disponibilizar na nuvem motores de transformacao de modelos, permitindo realizar gerenciamento de modelos de maneira independente