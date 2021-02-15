---
title: Modernizar seus aplicativos com o monitoramento e telemetria
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Modernizar seus aplicativos com monitoramento e telemetria
ms.date: 12/21/2020
ms.openlocfilehash: c79a16400ce9dadca50fabb6c7df2859e4519a41
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025232"
---
# <a name="modernize-your-apps-with-monitoring-and-telemetry"></a>Modernizar seus aplicativos com o monitoramento e telemetria

Quando você executa um aplicativo em produção, é essencial que você tenha informações sobre como seu aplicativo está sendo executado. Ele está sendo executado em um alto nível? Os usuários estão recebendo erros ou o aplicativo é estável e confiável? Você precisa de monitoramento avançado de desempenho, alertas avançados e painéis para ajudar a garantir que seu aplicativo esteja disponível e funcionando conforme o esperado. Você também precisa ser capaz de ver rapidamente se há um problema, determinar quantos clientes são afetados e executar uma análise de causa raiz para localizar e corrigir o problema.

## <a name="monitor-your-application-with-application-insights"></a>Monitore seu aplicativo com Application Insights

O Application Insights é um serviço de gerenciamento de desempenho de aplicativos (APM) extensível para desenvolvedores da Web que trabalham em várias plataformas. Use-o para monitorar seu aplicativo Web online. Application Insights detecta automaticamente anomalias de desempenho. Ele inclui ferramentas de análise poderosas para ajudá-lo a diagnosticar problemas e para ajudá-lo a entender o que os usuários realmente fazem com seu aplicativo. O Application Insights foi projetado para ajudar você a aprimorar continuamente o desempenho e a usabilidade do seu aplicativo. Ele funciona para aplicativos em uma ampla variedade de plataformas, incluindo .NET, Node.js e J2EE, seja hospedado localmente ou na nuvem. O Application Insights integra-se aos seus processos do DevOps e tem pontos de conexão para várias ferramentas de desenvolvimento.

A Figura 4-10 mostra um exemplo de como o Application Insights monitora o aplicativo e como ele o orienta a um painel.

![Captura de tela do painel de monitoramento de Application Insights.](./media/modernize-your-apps-with-monitoring-and-telemetry/application-insights-monitoring-dashboard.png)

**Figura 4-10.** Painel de monitoramento de Application Insights

## <a name="monitor-your-docker-infrastructure-with-log-analytics-and-its-container-monitoring-solution"></a>Monitorar sua infraestrutura do Docker com Log Analytics e sua solução de monitoramento de contêiner

O [Azure log Analytics](/azure/log-analytics/log-analytics-overview) faz parte do [Microsoft Azure solução de monitoramento geral](/azure/monitoring-and-diagnostics/monitoring-overview). Ele também é um serviço no [OMS (Operations Management Suite)](/azure/operations-management-suite/operations-management-suite-overview). O Log Analytics monitora ambientes locais e de nuvem (OMS para locais) para ajudar a manter a disponibilidade e o desempenho. Ele coleta dados gerados pelos recursos em seus ambientes de nuvem e locais e de outras ferramentas de monitoramento para fornecer análise de várias fontes.

Em relação aos logs de infraestrutura do Azure, Log Analytics, como um serviço do Azure, ingere dados de log e de métrica de outros serviços do Azure (via [Azure monitor](/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor)), VMS do Azure, contêineres do Docker e outras infraestruturas locais ou de nuvem. O Log Analytics oferece pesquisa de logs flexível e análise integrada sobre esses dados. Ele fornece ferramentas avançadas que você pode usar para analisar dados entre fontes, ele permite consultas complexas em todos os logs e pode alertar proativamente com base nas condições especificadas. Você pode até mesmo coletar dados personalizados no repositório Log Analytics central, onde você pode consultá-los e visualizá-los. Você também pode aproveitar as Log Analytics soluções internas para obter informações sobre a segurança e a funcionalidade da sua infraestrutura imediatamente.

Você pode acessar Log Analytics por meio do portal do OMS ou do portal do Azure, que são executados em qualquer navegador e fornecem acesso a definições de configuração e várias ferramentas para analisar e agir sobre os dados coletados.

A [solução de monitoramento de contêiner](/azure/log-analytics/log-analytics-containers) no log Analytics ajuda a exibir e gerenciar seus hosts de contêiner do Docker e do Windows em um único local. A solução mostra quais contêineres estão em execução, qual imagem de contêiner eles estão executando e onde os contêineres estão em execução. Você pode exibir informações de auditoria detalhadas, incluindo comandos que estão sendo usados com contêineres. Você também pode solucionar problemas de contêineres exibindo e pesquisando logs centralizados, sem a necessidade de exibir remotamente os hosts Docker ou Windows. Você pode encontrar contêineres que podem estar com ruídos e consumindo recursos em excesso em um host. Além disso, você pode exibir o uso centralizado de CPU, memória, armazenamento e rede e informações de desempenho para contêineres. Nos computadores que executam o Windows, você pode centralizar e comparar os logs do Windows Server, do Hyper-V e dos contêineres do Docker. A solução oferece suporte aos orquestradores de contêiner a seguir:

- Docker Swarm

- DC/OS

- Kubernetes

- Red Hat OpenShift

A Figura 4-11 mostra as relações entre vários hosts de contêiner e agentes e OMS.

![Captura de tela da solução de monitoramento de contêiner Log Analytics.](./media/modernize-your-apps-with-monitoring-and-telemetry/log-analytics-container-monitoring-solution.png)

**Figura 4-11.** Log Analytics solução de monitoramento de contêiner

Você pode usar a solução de monitoramento de contêiner Log Analytics para:

- Veja informações sobre todos os hosts de contêiner em um único local.

- Saiba quais contêineres estão em execução, qual imagem eles estão executando e onde estão em execução.

- Consulte uma trilha de auditoria para ações em contêineres.

- Solucione problemas exibindo e pesquisando logs centralizados sem fazer logon remoto nos hosts do Docker.

- Encontre contêineres que podem ser "vizinhos ruidosas" e consumindo recursos em excesso em um host.

- Exibir o uso centralizado de CPU, memória, armazenamento e rede e informações de desempenho para contêineres.

### <a name="additional-resources"></a>Recursos adicionais

- **Visão geral do monitoramento no Microsoft Azure**

<https://docs.microsoft.com/azure/azure-monitor/overview>

- **O que é o Application Insights?**

<https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview>

- **O que é o Log Analytics?**

<https://docs.microsoft.com/azure/log-analytics/log-analytics-overview>

- **Solução de monitoramento de contêiner no Azure Monitor**

<https://docs.microsoft.com/azure/azure-monitor/insights/containers>

- **Visão geral do Azure Monitor**

<https://docs.microsoft.com/azure/azure-monitor/overview>

- **O que é Operations Management Suite (OMS)?**

<https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview>

>[!div class="step-by-step"]
>[Anterior](build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud.md) 
> [Avançar](life-cycle-ci-cd-pipelines-devops-tools.md)
