---
title: Elasticsearch em aplicativos nativos de nuvem
description: Saiba mais sobre como adicionar recursos de pesquisa elástica a aplicativos nativos de nuvem.
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: fa46f3387eecb3fccd63fdea10c11e92923ae862
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91155374"
---
# <a name="elasticsearch-in-a-cloud-native-app"></a>Elasticsearch em um aplicativo nativo de nuvem

O Elasticsearch é um sistema de pesquisa e análise distribuído que permite recursos de pesquisa complexos em diferentes tipos de dados. É de código-fonte aberto e amplamente popular. Considere como as seguintes empresas integram o Elasticsearch em seus aplicativos:

- [Wikipédia](https://blog.wikimedia.org/2014/01/06/wikimedia-moving-to-elasticsearch/) para pesquisa de texto completo e incremental (Pesquisar ao digitar).
- [GitHub](https://www.elastic.co/customers/github) para indexar e expor mais de 8 milhões repositórios de código.  
- [Docker](https://www.elastic.co/customers/docker) para tornar sua biblioteca de contêineres detectável.

O Elasticsearch é criado sobre o mecanismo de pesquisa de texto completo do [Apache Lucene](https://lucene.apache.org/core/) . O Lucene fornece indexação e consulta de documentos de alto desempenho. Ele indexa dados com um esquema de indexação invertido – em vez de mapear páginas para palavras-chave, ele mapeia palavras-chave para páginas assim como um glossário no final de um livro. O Lucene tem recursos de sintaxe de consulta avançados e pode consultar dados por:

- Termo (uma palavra completa)
- Prefixo (começa com o Word)
- Curinga (usando os \* filtros "" ou "?")
- Frase (uma sequência de texto em um documento)
- Valor booliano (pesquisas complexas combinando consultas)

Embora o Lucene forneça um direcionamento de baixo nível para pesquisa, o Elasticsearch fornece o servidor que se encontra na parte superior do Lucene. O Elasticsearch adiciona funcionalidade de nível superior para simplificar o funcionamento do Lucene, incluindo uma API RESTful para acessar a funcionalidade de indexação e pesquisa do Lucene. Ele também fornece uma infraestrutura distribuída capaz de grande escalabilidade, tolerância a falhas e alta disponibilidade.

Para aplicativos nativos de nuvem maiores com requisitos de pesquisa complexos, o Elasticsearch está disponível como serviço gerenciado no Azure. O Microsoft Azure Marketplace apresenta modelos pré-configurados que os desenvolvedores podem usar para implantar um cluster Elasticsearch no Azure.

No Microsoft Azure Marketplace, os desenvolvedores podem usar modelos pré-configurados criados para implantar rapidamente um cluster Elasticsearch no Azure. Usando a oferta gerenciada pelo Azure, você pode implantar até 50 nós de dados, 20 nós coordenados e três nós mestres dedicados.

## <a name="summary"></a>Resumo

Este capítulo apresentou uma visão detalhada dos dados em sistemas nativos de nuvem. Começamos por contrastar o armazenamento de dados em aplicativos monolíticos com padrões de armazenamento de dados em sistemas nativos de nuvem. Examinamos os padrões de dados implementados em sistemas nativos de nuvem, incluindo consultas entre serviços, transações distribuídas e padrões para lidar com sistemas de alto volume. Nós contrastamos o SQL com dados NoSQL. Examinamos as opções de armazenamento de dados disponíveis no Azure que incluem opções centradas na Microsoft e em código aberto. Por fim, discutimos Caching e Elasticsearch em um aplicativo nativo de nuvem.

### <a name="references"></a>Referências

- [Padrão CQRS (Segregação de Responsabilidade de Consulta e Comando)](/azure/architecture/patterns/cqrs)

- [Padrão de fornecimento do evento](/azure/architecture/patterns/event-sourcing)

- [Por que a partição RDBMS não é tolerante a teorema em CAP e por que ela está disponível?](https://stackoverflow.com/questions/36404765/why-isnt-rdbms-partition-tolerant-in-cap-theorem-and-why-is-it-available)

- [Exibição Materializada](/azure/architecture/patterns/materialized-view)

- [Tudo o que você realmente precisa saber sobre bancos de dados de código-fonte aberto](https://www.ibm.com/blogs/systems/all-you-really-need-to-know-about-open-source-databases/)

- [Padrão de transação de compensação](/azure/architecture/patterns/compensating-transaction)

- [Padrão saga](https://microservices.io/patterns/data/saga.html)

- [Padrões de Saga | Como implementar transações de negócios usando microserviços](https://blog.couchbase.com/saga-pattern-implement-business-transactions-using-microservices-part/)

- [Padrão de transação de compensação](/azure/architecture/patterns/compensating-transaction)

- [Voltando para o 9-Ball: níveis de consistência de Cosmos DB explicados](https://blog.jeremylikness.com/blog/2018-03-23_getting-behind-the-9ball-cosmosdb-consistency-levels/)

- [Explorando os diferentes tipos de bancos de dados NoSQL parte II](https://www.3pillarglobal.com/insights/exploring-the-different-types-of-nosql-databases)

- [Nos bancos de dados RDBMS, NoSQL e NewSQL. Entrevista com John Ryan](http://www.odbms.org/blog/2018/03/on-rdbms-nosql-and-newsql-databases-interview-with-john-ryan/)
  
- [SQL vs NoSQL vs NewSQL: a comparação completa](https://www.xenonstack.com/blog/sql-vs-nosql-vs-newsql/)

- [DASH: quatro propriedades de bancos de dados kubernetes-Native](https://thenewstack.io/dash-four-properties-of-kubernetes-native-databases/)

- [CockroachDB](https://www.cockroachlabs.com/)

- [TiDB](https://pingcap.com/en/)

- [YugabyteDB](https://www.yugabyte.com/)

- [Vitess](https://vitess.io/)

- [Elasticsearch: o Guia Definitivo](https://shop.oreilly.com/product/0636920028505.do)
  
- [Introdução ao Apache Lucene](https://www.baeldung.com/lucene)

>[!div class="step-by-step"]
>[Anterior](azure-caching.md) 
> [Avançar](resiliency.md) <!-- Next Chapter -->
