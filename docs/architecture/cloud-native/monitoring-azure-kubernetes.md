---
title: Como monitorar nos Serviços de Kubernetes do Azure
description: Como monitorar nos Serviços de Kubernetes do Azure
ms.date: 01/19/2021
ms.openlocfilehash: d044337150edddac9e24218ccaeaace1f413e654
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506026"
---
# <a name="monitoring-in-azure-kubernetes-services"></a>Como monitorar nos Serviços de Kubernetes do Azure

O log interno em kubernetes é primitivo. No entanto, há algumas ótimas opções para fazer os logs de kubernetes e em um local onde eles podem ser analisados corretamente. Se você precisar monitorar os clusters do AKS, configurar a pilha elástica para kubernetes é uma ótima solução.

## <a name="azure-monitor-for-containers"></a>Azure Monitor para Contêineres

[Azure monitor para contêineres](/azure/azure-monitor/insights/container-insights-overview) dá suporte a logs de consumo não apenas kubernetes, mas também de outros mecanismos de orquestração, como DC/os, Docker Swarm e Red Hat OpenShift.

![Consumindo logs de vários contêineres, ](./media/containers-diagram.png)
 **Figura 7-10**. Consumindo logs de vários contêineres

O [Prometheus](https://prometheus.io/) é uma popular solução de monitoramento de métrica de software livre. Ele faz parte da base de computação nativa da nuvem. Normalmente, o uso de Prometheus requer o gerenciamento de um servidor Prometheus com seu próprio armazenamento. No entanto, [Azure monitor para contêineres fornece integração direta com pontos de extremidade de métricas do Prometheus](/azure/azure-monitor/insights/container-insights-prometheus-integration), portanto, um servidor separado não é necessário.

As informações de log e métricas são coletadas não apenas dos contêineres em execução no cluster, mas também dos hosts de cluster. Ele permite correlacionar as informações de log das duas tornando muito mais fácil rastrear um erro.

A instalação dos coletores de logs difere nos clusters do [Windows](/azure/azure-monitor/insights/containers#configure-a-log-analytics-windows-agent-for-kubernetes) e do [Linux](/azure/azure-monitor/insights/containers#configure-a-log-analytics-linux-agent-for-kubernetes) . Mas, em ambos os casos, a coleção de log é implementada como um [daemonset](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)kubernetes, o que significa que o coletor de logs é executado como um contêiner em cada um dos nós.

Não importa qual orquestrador ou sistema operacional está executando o daemon de Azure Monitor, as informações de log são encaminhadas para as mesmas ferramentas de Azure Monitor com as quais os usuários estão familiarizados. Essa abordagem garante uma experiência paralela em ambientes que combinam diferentes fontes de log, como um ambiente híbrido de kubernetes/Azure Functions.

![Um painel de exemplo mostrando informações de log e métrica de vários contêineres em execução. ](./media/containers-dashboard.png)
 **Figura 7-11**. Um painel de exemplo mostrando informações de log e métrica de muitos contêineres em execução.

## <a name="logfinalize"></a>Log. Finalize ()

O registro em log é uma das partes mais desprocuradas e, ainda mais importantes, da implantação de qualquer aplicativo em escala. À medida que o tamanho e a complexidade dos aplicativos aumentam, então a dificuldade de depurá-los. Ter os principais logs de qualidade disponíveis torna a depuração muito mais fácil e a move do território de "quase impossível" para "uma experiência agradável".

>[!div class="step-by-step"]
>[Anterior](logging-with-elastic-stack.md) 
> [Avançar](azure-monitor.md)
