---
title: Quando implantar Contêineres do Windows para VMs do Azure (nuvem de IaaS)
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Quando implantar contêineres do Windows em VMs do Azure (nuvem IaaS)
ms.date: 12/21/2020
ms.openlocfilehash: 64ba53fa56227266ee0e61a128d18373a2dbbc93
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025088"
---
# <a name="when-to-deploy-windows-containers-to-azure-vms-iaas-cloud"></a>Quando implantar Contêineres do Windows para VMs do Azure (nuvem de IaaS)

Se sua organização estiver usando VMs do Azure, mesmo se você também estiver usando contêineres do Windows, ainda estará lidando com IaaS. Isso significa que lidar com operações de infraestrutura, patches de sistema operacional de VM e complexidade de infraestrutura para aplicativos altamente escalonáveis quando você precisa implantar em várias VMs em uma infraestrutura de balanceamento de carga. Os principais cenários para usar contêineres do Windows em uma VM do Azure são:

- **Ambiente de desenvolvimento/teste**: uma VM na nuvem é perfeita para desenvolvimento e teste na nuvem. Você pode criar ou parar rapidamente o ambiente dependendo de suas necessidades.

- **Necessidades de escalabilidade pequenas e médias**: em cenários em que você pode precisar de apenas algumas VMs para seu ambiente de produção, o gerenciamento de algumas VMs pode ser acessível até que você possa mudar para ambientes PaaS mais avançados, como orquestradores.

- **Ambiente de produção com as ferramentas de implantação existentes**: você pode estar mudando de um ambiente local no qual você investiu em ferramentas para fazer implantações complexas em VMs ou servidores bare-metal (como Puppet ou ferramentas semelhantes). Para migrar para a nuvem com alterações mínimas nos procedimentos de implantação do ambiente de produção, você pode continuar a usar essas ferramentas para implantar nas VMs do Azure. No entanto, você desejará usar contêineres do Windows como a unidade de implantação para melhorar a experiência de implantação.

>[!div class="step-by-step"]
>[Anterior](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md) 
> [Avançar](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
