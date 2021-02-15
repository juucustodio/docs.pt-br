---
title: Modernizar o ciclo de vida do seu aplicativo com pipelines de CI/CD e ferramentas de DevOps na nuvem
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Modernizar o ciclo de vida de seu aplicativo com pipelines de CI/CD e ferramentas de DevOps na nuvem
ms.date: 12/21/2020
ms.openlocfilehash: f8517ebe8570b8d2be7b49c3cb9e1bc436076af2
ms.sourcegitcommit: 4f5f1855849cb02c3b610c7006ac21d7429f3348
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235333"
---
# <a name="modernize-your-apps-lifecycle-with-cicd-pipelines-and-devops-tools-in-the-cloud"></a>Modernizar o ciclo de vida do seu aplicativo com pipelines de CI/CD e ferramentas de DevOps na nuvem

As empresas de hoje precisam inovar em um ritmo rápido para serem competitivas no Marketplace. O fornecimento de aplicativos modernos de alta qualidade exige ferramentas e processos de DevOps que são essenciais para implementar esse ciclo constante de inovação. Com as ferramentas DevOps certas, os desenvolvedores podem simplificar a implantação contínua e obter aplicativos inovadores para as mãos de usuários mais rapidamente.

Embora as práticas de integração e implantação contínuas sejam bem estabelecidas, a introdução dos contêineres apresenta novas considerações, especialmente quando você está trabalhando com aplicativos com vários contêineres.

O Azure DevOps Services dá suporte à integração e à implantação contínuas de aplicativos de vários contêineres a vários ambientes por meio das tarefas oficiais de implantação de Azure DevOps Services:

- [Implantar em um Aplicativo Web para Contêineres do Azure](/azure/devops/pipelines/apps/cd/deploy-docker-webapp?tabs=dotnet-core)

- [Implantar no Serviço de Kubernetes do Azure](/azure/devops/pipelines/apps/cd/deploy-aks?tabs=dotnet-core)

Mas você também pode implantar no [Docker Swarm](https://blog.jcorioland.io/archives/2016/11/29/full-ci-cd-pipeline-to-deploy-multi-containers-application-on-azure-container-service-docker-swarm-using-visual-studio-team-services.html) ou DC/OS usando Azure DevOps Services tarefas baseadas em script.

Para continuar a facilitar a agilidade da implantação, essas ferramentas fornecem excelentes experiências de implantação de desenvolvimento para teste para produção para cargas de trabalho de contêiner, com uma opção de desenvolvimento e soluções de CI/CD.

A Figura 4-12 mostra um pipeline de implantação contínua que é implantado em um cluster kubernetes no serviço de contêiner do Azure.

![Captura de tela de Azure DevOps Services implantando em um cluster kubernetes.](./media/life-cycle-ci-cd-pipelines-devops-tools/deploy-mvc-app-container-kubernetes.png)

**Figura 4-12.** Azure DevOps Services pipeline de implantação contínua, implantando em um cluster kubernetes

>[!div class="step-by-step"]
>[Anterior](modernize-your-apps-with-monitoring-and-telemetry.md) 
> [Avançar](migrate-to-hybrid-cloud-scenarios.md)
