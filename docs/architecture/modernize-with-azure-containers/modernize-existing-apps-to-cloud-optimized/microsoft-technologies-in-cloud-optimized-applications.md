---
title: Tecnologias da Microsoft em aplicativos otimizados para nuvem
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Tecnologias da Microsoft em aplicativos otimizados para nuvem
ms.date: 04/28/2018
ms.openlocfilehash: b257497835638dd65c894998e95bd7e9d784b7bf
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172008"
---
# <a name="microsoft-technologies-in-cloud-optimized-applications"></a>Tecnologias da Microsoft em aplicativos otimizados para nuvem

A lista a seguir descreve as ferramentas, as tecnologias e as soluções que são reconhecidas como requisitos para aplicativos otimizados para a nuvem. Você pode adotar elementos otimizados para a nuvem de forma seletiva ou gradual, dependendo de suas prioridades.

- **Infraestrutura de nuvem**: a infraestrutura que fornece a plataforma de computação, o sistema operacional, a rede e o armazenamento. Microsoft Azure está posicionado nesse nível.

- **Tempo de execução**: essa camada fornece o ambiente para que o aplicativo seja executado. Se você estiver usando contêineres, essa camada geralmente se baseará no [mecanismo do Docker](https://docs.docker.com/engine/), em execução em hosts Linux ou em hosts do Windows. (Há suporte para[contêineres do Windows](/virtualization/windowscontainers/about/) a partir do Windows Server 2016. Contêineres do Windows é a melhor opção para aplicativos de .NET Framework existentes que são executados no Windows.)

- **Nuvem gerenciada**: ao escolher uma opção de nuvem gerenciada, você pode evitar a despesa e a complexidade de gerenciar e dar suporte à infraestrutura subjacente, às VMs, aos patches do sistema operacional e à configuração de rede. Se você optar por migrar usando IaaS, será responsável por todas essas tarefas e pelos custos associados. Em uma opção de nuvem gerenciada, você gerencia apenas os aplicativos e serviços que você desenvolve. O provedor de serviços de nuvem geralmente gerencia todo o resto. Exemplos de serviços de nuvem gerenciados no Azure incluem [banco de dados SQL do Azure](https://azure.microsoft.com/services/sql-database), [cache Redis do Azure](https://azure.microsoft.com/services/cache/), [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), [armazenamento do Azure](https://azure.microsoft.com/services/storage/), [banco de dados do Azure para MySQL](https://azure.microsoft.com/services/mysql/), [banco de dados do Azure para PostgreSQL](https://azure.microsoft.com/services/postgresql/), [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)e serviços de computação gerenciados, como [conjuntos de dimensionamento de VM](https://azure.microsoft.com/services/virtual-machine-scale-sets/), serviço de [Azure app](https://azure.microsoft.com/services/app-service/)e [serviço kubernetes do Azure](https://azure.microsoft.com/services/container-service/).

- **Desenvolvimento de aplicativos**: você pode escolher entre vários idiomas ao criar aplicativos que são executados em contêineres. Este guia se concentra no [.net](https://dotnet.microsoft.com), mas você pode desenvolver aplicativos baseados em contêiner usando outras linguagens, como Node.js, Python, Spring/Java ou go.

- **Monitoramento, telemetria, registro em log e auditoria**: a capacidade de monitorar e auditar aplicativos e contêineres em execução na nuvem é essencial para qualquer aplicativo otimizado para a nuvem. [Aplicativo Azure informações](https://azure.microsoft.com/services/application-insights/) e [Microsoft Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) são as principais ferramentas da Microsoft que fornecem monitoramento e auditoria para aplicativos otimizados para a nuvem.

- **Provisionamento**: as ferramentas de automação ajudam você a provisionar a infraestrutura e a implantar um aplicativo em vários ambientes (produção, teste, preparo). Você pode usar ferramentas como chefe e Puppet para gerenciar a configuração e o ambiente de um aplicativo. Essa camada também pode ser implementada usando abordagens mais simples e diretas. Por exemplo, você pode implantar diretamente usando as ferramentas da interface de linha de comando do Azure (CLI do Azure) e, em seguida, usar os pipelines de implantação contínua e gerenciamento de liberação no [Azure DevOps Services](https://azure.microsoft.com/services/devops/).

- **Ciclo de vida do aplicativo**: [Azure DevOps Services](https://azure.microsoft.com/services/devops/) e outras ferramentas, como Jenkins, são servidores de automação criados que ajudam a implementar pipelines de CI/CD, incluindo o gerenciamento de liberações.

As próximas seções deste capítulo e as orientações relacionadas, concentram-se especificamente nos detalhes sobre a camada de tempo de execução (contêineres do Windows). A orientação descreve as maneiras como você pode implantar contêineres do Windows em VMs do Windows Server 2016 (e versões posteriores) e instâncias de contêiner do Azure. Ele também aborda plataformas mais avançadas de PaaS, como o serviço Azure App e o Orchestrator, como o serviço kubernetes do Azure.

## <a name="monolithic-applications-can-be-cloud-optimized"></a>Os aplicativos monolíticos *podem* ser otimizados para a nuvem

É importante destacar que os aplicativos monolíticos (aplicativos que não são baseados em microserviços) *podem* ser aplicativos otimizados para a nuvem. Você pode criar e operar aplicativos monolíticos que aproveitam o modelo de computação em nuvem usando uma combinação de contêineres, entrega contínua e DevOps. Se um aplicativo monolítico existente for adequado para suas metas de negócios, você poderá modernizar e torná-lo otimizado para a nuvem.

Da mesma forma, se os aplicativos monolíticos puderem ser aplicativos otimizados para nuvem, outras arquiteturas mais complexas, como aplicativos de N camadas, também podem ser modernizadas como aplicativos otimizados para a nuvem.

>[!div class="step-by-step"]
>[Anterior](reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications.md) 
> [Avançar](what-about-cloud-native-applications.md)
