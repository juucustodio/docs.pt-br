---
title: Escala de contêineres e aplicativos sem servidor
description: Dimensionamento de aplicativos nativos de nuvem com o serviço kubernetes do Azure para atender à demanda do usuário.
ms.date: 05/13/2020
ms.openlocfilehash: edf56ba50ba391e06e588d682918cd473a2cf374
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91165973"
---
# <a name="scaling-containers-and-serverless-applications"></a>Escala de contêineres e aplicativos sem servidor

Há duas maneiras de dimensionar um aplicativo: para cima ou para fora. O primeiro se refere à adição de capacidade a um único recurso, enquanto o último se refere à adição de mais recursos para aumentar a capacidade.

## <a name="the-simple-solution-scaling-up"></a>A solução simples: escalar verticalmente

A atualização de um servidor de host existente com CPU, memória, velocidade de e/s de disco aumentada e velocidade de e/s de rede é conhecida como *escalar verticalmente*. Escalar verticalmente um aplicativo nativo de nuvem envolve a escolha de recursos mais capacitados do fornecedor de nuvem. Por exemplo, você pode um novo pool de nós com VMs maiores em seu cluster kubernetes. Em seguida, migre seus serviços em contêineres para o novo pool.

Aplicativos sem servidor expandem verticalmente, escolhendo o [plano de funções Premium](/azure/azure-functions/functions-scale) ou os tamanhos de instância Premium de um plano do serviço de aplicativo dedicado.

## <a name="scaling-out-cloud-native-apps"></a>Expandindo aplicativos nativos de nuvem

Aplicativos nativos de nuvem geralmente experimentam flutuações grandes na demanda e exigem escala em um momento. Eles favorecem a expansão. A expansão é feita horizontalmente com a adição de computadores adicionais (chamados nós) ou instâncias de aplicativo a um cluster existente. No kubernetes, você pode dimensionar manualmente ajustando as definições de configuração para o aplicativo (por exemplo, [dimensionando um pool de nós](/azure/aks/use-multiple-node-pools#scale-a-node-pool-manually)) ou por meio do dimensionamento automático.

Os clusters AKS podem ser dimensionados automaticamente de uma das duas maneiras:

Primeiro, a [escala automática de Pod horizontal](/azure/aks/tutorial-kubernetes-scale#autoscale-pods) monitora a demanda de recursos e dimensiona automaticamente suas réplicas de pod para atendê-las. Quando o tráfego aumenta, as réplicas adicionais são provisionadas automaticamente para escalar horizontalmente seus serviços. Da mesma forma, quando a demanda diminui, elas são removidas para reduzir seus serviços. Você define a métrica na qual dimensionar, por exemplo, o uso da CPU. Você também pode especificar o número mínimo e máximo de réplicas a serem executadas. O AKS monitora essa métrica e dimensiona de acordo.

Em seguida, o recurso de [dimensionamento automático do cluster AKs](/azure/aks/cluster-autoscaler) permite que você dimensione automaticamente os nós de computação em um cluster kubernetes para atender à demanda. Com ele, você pode adicionar automaticamente novas VMs ao conjunto de dimensionamento de máquinas virtuais do Azure subjacente sempre que mais capacidade de computação do for necessária. Ele também remove nós quando não é mais necessário.

A Figura 3-13 mostra a relação entre esses dois serviços de dimensionamento.

![Dimensionando um plano do serviço de aplicativo.](./media/aks-cluster-autoscaler.png)

**Figura 3-13**. Dimensionando um plano do serviço de aplicativo.

Trabalhando juntos, ambos garantem um número ideal de instâncias de contêiner e nós de computação para dar suporte à demanda flutuante. A escala automática de Pod horizontal otimiza o número de pods necessário. O dimensionador automática de cluster otimiza o número de nós necessários.

### <a name="scaling-azure-functions"></a>Dimensionamento do Azure Functions

Azure Functions escalar horizontalmente automaticamente sob demanda. Os recursos do servidor são alocados e removidos dinamicamente com base no número de eventos disparados. Você é cobrado apenas pelos recursos de computação consumidos quando suas funções são executadas. A cobrança é baseada no número de execuções, no tempo de execução e na memória usada.

Embora o plano de consumo padrão forneça uma solução econômica e escalonável para a maioria dos aplicativos, a opção Premium permite que os desenvolvedores tenham flexibilidade para requisitos de Azure Functions personalizados. A atualização para o plano Premium fornece controle sobre os tamanhos de instância, instâncias pré-configuradas (para evitar atrasos de inicialização a frio) e VMs dedicadas.

>[!div class="step-by-step"]
>[Anterior](deploy-containers-azure.md) 
> [Avançar](other-deployment-options.md)
