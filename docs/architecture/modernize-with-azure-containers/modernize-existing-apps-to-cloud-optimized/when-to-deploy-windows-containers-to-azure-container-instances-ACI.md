---
title: Quando implantar contêineres do Windows em ACI (instâncias de contêiner do Azure)
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Quando implantar contêineres do Windows em ACI (instâncias de contêiner do Azure)
ms.date: 12/21/2020
ms.openlocfilehash: 556fe7cbec7d259db9ec886b777feda9eed09116
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025127"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-instances-aci"></a>Quando implantar contêineres do Windows em ACI (instâncias de contêiner do Azure)

A principal proposta de valor das instâncias de contêiner do Azure é que você pode imediatamente implantar contêineres nela e não precisa manter esse ambiente, não é necessário atualizar/corrigir o sistema operacional ou as VMs subjacentes, tudo isso é transparente e apenas implantar contêineres em um ambiente pronto para uso.

Os motivos e cenários em que você desejaria usar o ACI são semelhantes aos principais cenários quando você usa VMs do Azure com contêineres, portanto, basicamente, os principais cenários para usar as instâncias de contêiner do Azure são:

- **Cenários de desenvolvimento/teste**
- **Automação de tarefas**
- **Agentes de CI/CD**
- **Processamento em lotes de pequena/escala**
- **Aplicativos Web simples**

O cenário de aplicativos Web simples é um cenário justo para ACI, mas leve em conta que, desde o ACI, você só pode ter uma única instância de contêiner por imagem de contêiner, não terá alta disponibilidade e terá apenas escalabilidade limitada.

No entanto, mesmo quando o ACI é considerado uma infraestrutura porque ele apenas fornece instâncias de contêiner único, há um grande benefício em comparação com as VMs regulares do Azure com o Windows Server. Com o ACI, você apenas implanta os contêineres em um ambiente automantido e só paga por esses contêineres. Você não precisa manter/atualizar/corrigir VMs, portanto é uma plataforma muito melhor para a maioria dos cenários em que você pode estar usando VMs com contêineres. Usar o ACI é um avanço direto, você simplesmente implanta um contêiner, não há necessidade de criar um ambiente de VM que você apenas implante contêineres.

Os principais benefícios das ACI (instâncias de contêiner do Azure) são:

- Executar contêineres sem gerenciar servidores
- Aumentar a agilidade com contêineres sob demanda
- Implante contêineres na nuvem com simplicidade e velocidade sem precedentes, com um único comando.
- Proteger aplicativos com isolamento de hipervisor

Em suma, com o ACI, você pode desenvolver aplicativos rapidamente sem gerenciar máquinas virtuais ou ter que aprender novas ferramentas. É apenas seu aplicativo, em um contêiner, em execução na nuvem.

> [!div class="step-by-step"]
> [Anterior](when-to-deploy-windows-containers-to-azure-vms-iaas-cloud.md) 
>  [Avançar](when-to-deploy-windows-containers-to-azure-container-service-kubernetes.md)
