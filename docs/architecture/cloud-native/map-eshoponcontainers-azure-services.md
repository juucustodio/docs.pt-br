---
title: Como mapear o eShopOnContainers para os Serviços do Azure
description: Mapeamento de eShopOnContainers para serviços do Azure, como o serviço kubernetes do Azure, o gateway de API e o barramento de serviço do Azure.
ms.date: 01/19/2021
ms.openlocfilehash: aa0d5cc3bf6c0226627ce558606f974b0e7ec238
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506247"
---
# <a name="mapping-eshoponcontainers-to-azure-services"></a>Como mapear o eShopOnContainers para os Serviços do Azure

Embora não seja necessário, o Azure é bem adequado para dar suporte ao eShopOnContainers porque o projeto foi criado para ser um aplicativo nativo de nuvem. O aplicativo é criado com o .NET, para que possa ser executado em contêineres do Linux ou do Windows, dependendo do host do Docker. O aplicativo é composto por vários microserviços autônomos, cada um com seus próprios dados. Os diferentes microserviços demonstram abordagens diferentes, desde operações CRUD simples a padrões DDD e CQRS mais complexos. Os microserviços se comunicam com clientes via HTTP e uns com os outros por meio de comunicação baseada em mensagem. O aplicativo também dá suporte a várias plataformas para clientes, já que ele adota o HTTP como um protocolo de comunicação padrão e inclui aplicativos móveis ASP.NET Core e Xamarin que são executados em plataformas Android, iOS e Windows.

A arquitetura do aplicativo é mostrada na Figura 2-5. À esquerda estão os aplicativos cliente, divididos em tipos móveis, da Web tradicional e de SPA (aplicativo de página única) da Web. À direita estão os componentes do lado do servidor que compõem o sistema, cada um deles pode ser hospedado em contêineres e clusters kubernetes do Docker. O aplicativo Web tradicional é fornecido pela plataforma de ASP.NET Core aplicativos MVC mostrados em amarelo. Esse aplicativo e os aplicativos de SPA móveis e da Web se comunicam com os microserviços individuais por meio de um ou mais gateways de API. Os gateways de API seguem o padrão de "back-ends para front-ends" (BFF), o que significa que cada gateway é projetado para dar suporte a um determinado cliente front-end. Os microserviços individuais são listados à direita dos gateways de API e incluem a lógica de negócios e algum tipo de armazenamento de persistência. Os diferentes serviços fazem uso de bancos de dados SQL Server, instâncias de cache Redis e armazenamentos MongoDB/CosmosDB. Na extrema direita, está o barramento de evento do sistema, que é usado para a comunicação entre os microserviços.

![Arquitetura eShopOnContainers ](./media/eshoponcontainers-architecture.png)
 **Figura 2-5**. A arquitetura eShopOnContainers.

Todos os componentes do lado do servidor dessa arquitetura são mapeados facilmente para os serviços do Azure.

## <a name="container-orchestration-and-clustering"></a>Orquestração de contêineres e clustering

Os serviços hospedados por contêiner do aplicativo, de ASP.NET Core aplicativos MVC para os microserviços de catálogo individual e ordenação, podem ser hospedados e gerenciados no AKS (serviço kubernetes do Azure). O aplicativo pode ser executado localmente no Docker e no kubernetes, e os mesmos contêineres podem ser implantados em ambientes de produção e de preparo hospedados em AKS. Esse processo pode ser automatizado, como veremos na próxima seção.

O AKS fornece serviços de gerenciamento para clusters individuais de contêineres. O aplicativo implantará contêineres separados para cada microserviço no cluster AKS, conforme mostrado no diagrama de arquitetura acima. Essa abordagem permite que cada serviço individual seja dimensionado de forma independente de acordo com suas demandas de recursos. Cada microserviço também pode ser implantado de forma independente e, teoricamente, essas implantações devem incorrer em tempo de inatividade do sistema

## <a name="api-gateway"></a>Gateway de API

O aplicativo eShopOnContainers tem vários clientes front-end e vários serviços de back-end diferentes. Não há nenhuma correspondência de um para um entre os aplicativos cliente e os microserviços que dão suporte a eles. Nesse cenário, pode haver grande complexidade ao escrever software cliente para interface com os vários serviços de back-end de maneira segura. Cada cliente precisaria abordar essa complexidade por conta própria, resultando em duplicação e em vários lugares nos quais fazer atualizações à medida que os serviços mudam ou novas políticas são implementadas.

O APIM (gerenciamento de API do Azure) ajuda as organizações a publicar APIs de maneira consistente e gerenciável. O APIM consiste em três componentes: o gateway de API e o portal de administração (o portal do Azure) e um portal do desenvolvedor.

O gateway de API aceita chamadas à API e as roteia para a API de back-end apropriada. Ele também pode fornecer serviços adicionais, como verificação de chaves de API ou tokens JWT e transformação de API em tempo real sem modificações de código (por exemplo, para acomodar clientes que esperam uma interface mais antiga).

O portal do Azure é onde você define o esquema de API e empacota diferentes APIs em produtos. Você também configura o acesso do usuário, exibe relatórios e configura políticas para cotas ou transformações.

O portal do desenvolvedor serve como o principal recurso para os desenvolvedores. Ele fornece aos desenvolvedores documentação de API, um console de teste interativo e relatórios sobre seu próprio uso. Os desenvolvedores também usam o portal para criar e gerenciar suas próprias contas, incluindo suporte a assinatura e chave de API.

Usando o APIM, os aplicativos podem expor vários grupos diferentes de serviços, cada um fornecendo um back-end para um cliente de front-end específico. APIM é recomendado para cenários complexos. Para necessidades mais simples, o Ocelot de gateway de API leve pode ser usado. O aplicativo eShopOnContainers usa Ocelot devido à sua simplicidade e porque pode ser implantado no mesmo ambiente de aplicativo que o próprio aplicativo. [Saiba mais sobre eShopOnContainers, APIM e Ocelot.](../microservices/architect-microservice-container-applications/direct-client-to-microservice-communication-versus-the-api-gateway-pattern.md#azure-api-management)

Outra opção se seu aplicativo estiver usando o AKS é implantar o controlador de entrada do gateway do Azure como um pod no cluster do AKS. Essa abordagem permite que o cluster se integre a um gateway de Aplicativo Azure, permitindo que o gateway Equilibre a carga do tráfego para o pods AKS. [Saiba mais sobre o controlador de entrada do gateway do Azure para AKs](https://github.com/Azure/application-gateway-kubernetes-ingress).

## <a name="data"></a>Dados

Os vários serviços de back-end usados pelo eShopOnContainers têm requisitos de armazenamento diferentes. Vários microserviços usam bancos de dados SQL Server. O microserviço da cesta utiliza um cache Redis para sua persistência. O microserviço de locais espera uma API do MongoDB para seus dados. O Azure dá suporte a cada um desses formatos de dados.

Para SQL Server suporte a banco de dados, o Azure tem produtos para tudo, desde bancos de dados individuais até pools elásticos de banco de dados SQL altamente escalonáveis. Os microserviços individuais podem ser configurados para se comunicar com seus próprios bancos de dados individuais SQL Server de forma rápida e fácil. Esses bancos de dados podem ser dimensionados conforme necessário para dar suporte a cada microserviço separado de acordo com suas necessidades.

O aplicativo eShopOnContainers armazena a cesta de compras atual do usuário entre as solicitações. Esse aspecto é gerenciado pelo microserviço Basket que armazena os dados em um cache Redis. No desenvolvimento, esse cache pode ser implantado em um contêiner, enquanto em produção pode utilizar o cache do Azure para Redis. O cache do Azure para Redis é um serviço totalmente gerenciado que oferece alto desempenho e confiabilidade sem a necessidade de implantar e gerenciar instâncias ou contêineres do Redis por conta própria.

O microserviço de locais usa um banco de dados NoSQL do MongoDB para sua persistência. Durante o desenvolvimento, o banco de dados pode ser implantado em seu próprio contêiner, enquanto em produção o serviço pode aproveitar a [API do Azure Cosmos DB para MongoDB](/azure/cosmos-db/mongodb-introduction). Um dos benefícios da Azure Cosmos DB é sua capacidade de aproveitar vários protocolos de comunicação diferentes, incluindo uma API do SQL e APIs NoSQL comuns, incluindo MongoDB, Cassandra, Gremlin e armazenamento de tabelas do Azure. O Azure Cosmos DB oferece um banco de dados totalmente gerenciado e globalmente distribuído como um serviço que pode ser dimensionado para atender às necessidades dos serviços que o utilizam.

Os dados distribuídos em aplicativos nativos de nuvem são abordados em mais detalhes no [capítulo 5](distributed-data.md).

## <a name="event-bus"></a>Barramento de evento

O aplicativo usa eventos para comunicar alterações entre diferentes serviços. Essa funcionalidade pode ser implementada com várias implementações e localmente o aplicativo eShopOnContainers usa [RabbitMQ](https://www.rabbitmq.com/). Quando hospedado no Azure, o aplicativo aproveitará o [barramento de serviço do Azure](/azure/service-bus/) para suas mensagens. O barramento de serviço do Azure é um agente de mensagem de integração totalmente gerenciado que permite que aplicativos e serviços se comuniquem uns com os outros de uma maneira desacoplada, confiável e assíncrona. O barramento de serviço do Azure dá suporte a filas individuais, bem como a *Tópicos* separados para dar suporte a cenários de assinante do Publicador. O aplicativo eShopOnContainers aproveitará os tópicos com o barramento de serviço do Azure para dar suporte à distribuição de mensagens de um microserviço para qualquer outro microserviço que precisava reagir a uma determinada mensagem.

## <a name="resiliency"></a>Resiliência

Depois de implantado em produção, o aplicativo eShopOnContainers seria capaz de aproveitar vários serviços do Azure disponíveis para melhorar sua resiliência. O aplicativo publica verificações de integridade, que podem ser integradas com Application Insights para fornecer relatórios e alertas com base na disponibilidade do aplicativo. Os recursos do Azure também fornecem logs de diagnóstico que podem ser usados para identificar e corrigir erros e problemas de desempenho. Os logs de recursos fornecem informações detalhadas sobre quando e como os diferentes recursos do Azure são usados pelo aplicativo. Você aprenderá mais sobre os recursos de resiliência nativa de nuvem no [capítulo 6](resiliency.md).

>[!div class="step-by-step"]
>[Anterior](introduce-eshoponcontainers-reference-app.md) 
> [Avançar](deploy-eshoponcontainers-azure.md)
