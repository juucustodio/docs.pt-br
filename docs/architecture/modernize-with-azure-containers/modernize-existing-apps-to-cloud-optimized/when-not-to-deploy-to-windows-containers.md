---
title: Quando não implantar Contêineres do Windows
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Quando não implantar em contêineres do Windows
ms.date: 12/21/2020
ms.openlocfilehash: 4eea24ab8deb3719c778b45b3ddc1309277a3f50
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025167"
---
# <a name="when-not-to-deploy-to-windows-containers"></a>Quando não implantar Contêineres do Windows

Não há suporte para algumas tecnologias do Windows nos contêineres do Windows. Nesses casos, você ainda precisa migrar para as VMs de padrões, geralmente com apenas Windows e IIS.

Não há suporte para casos em contêineres do Windows, a partir de maio de 2018:

- O serviço de enfileiramento de mensagens da Microsoft (MSMQ) atualmente só está disponível em contêineres do Windows com base na versão v1803 do Windows Server, mas não em outras versões anteriores.

  - [Fórum de solicitações do UserVoice](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/15719031-create-base-container-image-with-msmq-server)

  - [O fórum de discussão](https://social.msdn.microsoft.com/Forums/bce99a7d-aa60-44fa-a348-450855650810/msmqserver-is-it-supported?forum=windowscontainers)

- No momento, não há suporte para o Microsoft Coordenador de Transações Distribuídas (MSDTC) em contêineres do Windows.

  - [Problema do GitHub](https://github.com/MicrosoftDocs/Virtualization-Documentation/issues/494)

- Microsoft Office atualmente não oferece suporte a contêineres.

  - [Fórum de solicitações do UserVoice](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/19686220-provide-office-support-for-containers)

- Os aplicativos de IU (aplicativos cliente com uma interface do usuário Visual) não são cenários com suporte.

- As funções de infraestrutura do Windows (DNS, DHCP, DC, NTP, PRINT, servidor de arquivos, IAM etc.) não são cenários com suporte.

Para outros cenários e solicitações sem suporte da Comunidade, consulte o fórum do UserVoice para contêineres do Windows: <https://windowsserver.uservoice.com/forums/304624-containers> .

### <a name="additional-resources"></a>Recursos adicionais

- **Máquinas virtuais e contêineres no Azure**

    <https://azure.microsoft.com/overview/containers/>

> [!div class="step-by-step"]
> [Anterior](deploy-existing-net-apps-as-windows-containers.md) 
>  [Avançar](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)
