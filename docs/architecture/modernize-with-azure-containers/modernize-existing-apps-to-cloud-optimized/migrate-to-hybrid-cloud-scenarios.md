---
title: Migrar para cenários de nuvem híbrida
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Migrar para cenários de nuvem híbrida
ms.date: 12/21/2020
ms.openlocfilehash: d5bf7f08381f3718061742b37c73604d8e57f1e2
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025219"
---
# <a name="migrate-to-hybrid-cloud-scenarios"></a>Migrar para cenários de nuvem híbrida

Algumas organizações e empresas não podem migrar alguns de seus aplicativos para nuvens públicas como Microsoft Azure ou qualquer outra nuvem pública devido a regulamentos ou suas próprias políticas. No entanto, é provável que qualquer organização possa se beneficiar de ter alguns de seus aplicativos na nuvem pública e em outros aplicativos locais. Mas um ambiente misto pode levar a uma complexidade excessiva em ambientes devido a diferentes plataformas e tecnologias usadas em nuvens públicas versus ambientes locais.

A Microsoft fornece a melhor solução de nuvem híbrida, uma na qual você pode otimizar seus ativos existentes no local e na nuvem pública, enquanto garante a consistência em uma nuvem híbrida do Azure. Você pode maximizar as habilidades existentes e obter uma abordagem flexível e unificada para a criação de aplicativos que podem ser executados na nuvem ou no local, graças a Azure Stack (local) e ao Azure (nuvem pública).

Quando se trata de segurança, você pode centralizar o gerenciamento e a segurança em sua nuvem híbrida. Você pode obter controle sobre todos os ativos, desde seu datacenter até a nuvem, fornecendo logon único para aplicativos locais e na nuvem. Você realiza essa funcionalidade estendendo Active Directory para uma nuvem híbrida e usando o gerenciamento de identidades.

Por fim, você pode distribuir e analisar os dados diretamente, usar as mesmas linguagens de consulta para ativos locais e de nuvem e aplicar análise e aprendizado profundo no Azure para enriquecer seus dados, independentemente de sua origem.

## <a name="azure-stack"></a>Azure Stack Hub

O Azure Stack é uma plataforma de nuvem híbrida que permite que você forneça serviços do Azure do datacenter da sua organização. O Azure Stack foi projetado para dar suporte a novas opções para seus aplicativos modernos em cenários importantes, como ambientes de borda e desconectado, ou atender aos requisitos específicos de segurança e conformidade.

A Figura 4-13 mostra uma visão geral da verdadeira plataforma de nuvem híbrida que a Microsoft oferece.

![Diagrama da plataforma de nuvem híbrida da Microsoft com o Azure Stack e o Azure.](./media/migrate-to-hybrid-cloud-scenarios/microsoft-hybrid-cloud-platform.png)

**Figura 4-13.** Plataforma de nuvem híbrida da Microsoft com Azure Stack e Azure

O Azure Stack é oferecido em duas opções de implantação para atender às suas necessidades:

- Sistemas integrados Azure Stack

- Kit de Desenvolvimento do Azure Stack

### <a name="azure-stack-integrated-systems"></a>Sistemas integrados Azure Stack

Azure Stack sistemas integrados são oferecidos por meio de uma parceria de parceiros de hardware e da Microsoft. A parceria cria uma solução que oferece inovação no ritmo da nuvem que é equilibrada com simplicidade no gerenciamento. Como o Azure Stack é oferecido como um sistema integrado de hardware e software, você obtém a quantidade certa de flexibilidade e controle, enquanto ainda adota a inovação a partir da nuvem. Azure Stack intervalo de sistemas integrados de tamanho de 4 a 12 nós e tem suporte em conjunto pelo parceiro de hardware e pela Microsoft. Use Azure Stack sistemas integrados para implementar novos cenários para suas cargas de trabalho de produção.

### <a name="azure-stack-development-kit"></a>Kit de Desenvolvimento do Azure Stack

O Kit de Desenvolvimento do Microsoft Azure Stack é uma implantação de nó único do Azure Stack que você pode usar para avaliar e saber mais sobre essa extensão. Você também pode usar Kit de Desenvolvimento do Azure Stack como um ambiente de desenvolvedor, no qual você pode desenvolver usando APIs e ferramentas que são consistentes com o Azure. O Kit de Desenvolvimento do Azure Stack não foi projetado para ser usado como um ambiente de produção.

### <a name="additional-resources"></a>Recursos adicionais

- **Nuvem híbrida do Azure**

    <https://azure.microsoft.com/overview/hybrid-cloud/>

- **Azure Stack**

    <https://azure.microsoft.com/overview/azure-stack/>

- **Contas de serviço do Active Directory para contêineres do Windows**

    <https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts>

- **Criar um contêiner com suporte a Active Directory**

    <https://docs.microsoft.com/archive/blogs/containerstuff/create-a-container-with-active-directory-support>

- **Licenciamento de Benefício Híbrido do Azure**

    <https://azure.microsoft.com/pricing/hybrid-benefit/>

>[!div class="step-by-step"]
>[Anterior](life-cycle-ci-cd-pipelines-devops-tools.md) 
> [Avançar](../walkthroughs-technical-get-started-overview.md)
