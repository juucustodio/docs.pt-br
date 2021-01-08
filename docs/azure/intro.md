---
title: Introdução ao Azure e ao .NET
description: Conheça o básico que você precisa saber sobre o Azure e o .NET.
ms.date: 06/20/2020
ms.topic: conceptual
ms.custom: devx-track-dotnet
ms.author: daberry
author: daberry
ms.openlocfilehash: b5766012b77da88ae9a696939b6e498ebc421522
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025036"
---
# <a name="introduction-to-azure-and-net"></a>Introdução ao Azure e ao .NET

## <a name="what-is-azure"></a>O que é o Azure?

O Azure é uma plataforma de nuvem projetada para simplificar o processo de criação de aplicativos modernos.  Independentemente de você optar por hospedar aplicativos totalmente no Azure ou estender seus aplicativos locais com os serviços do Azure, o Azure ajuda a criar aplicativos escalonáveis, confiáveis e que podem ser mantidos.  Com amplo suporte em ferramentas que você já usa como o Visual Studio e Visual Studio Code e uma biblioteca SDK abrangente, o Azure foi projetado para tornar você o desenvolvedor do .NET tão produtivo desde o início.

## <a name="application-development-scenarios-on-azure"></a>Cenários de desenvolvimento de aplicativos no Azure

Você pode incorporar o Azure ao seu aplicativo de diferentes maneiras, dependendo de suas necessidades.

- **Hospedagem de aplicativos no Azure-** O Azure pode hospedar toda a pilha de aplicativos de aplicativos Web e APIs para os bancos de dados para serviços de armazenamento. O Azure dá suporte a uma variedade de modelos de Hospedagem de serviços totalmente gerenciados para contêineres para máquinas virtuais. Ao usar serviços do Azure totalmente gerenciados, seus aplicativos podem aproveitar a escalabilidade, alta disponibilidade e segurança interna do Azure.

- **Consumindo serviços de nuvem de aplicativos-** Os aplicativos existentes podem incorporar os serviços do Azure para estender seus recursos.  Isso pode incluir a adição de recursos de pesquisa de texto completo com o [Azure pesquisa cognitiva](/azure/search/search-what-is-azure-search), o armazenamento seguro de segredos do aplicativo em [Azure Key Vault](/azure/key-vault/) ou a adição de recursos de visão, fala e reconhecimento de linguagem com os [Serviços cognitivas do Azure](/azure/cognitive-services/).  Esses serviços são totalmente gerenciados pelo Azure e podem ser facilmente adicionados ao seu aplicativo sem alterar a arquitetura atual do aplicativo ou o modelo de implantação.

- **Arquiteturas modernas sem servidor-** Azure Functions simplificar a criação de soluções para lidar com fluxos de trabalho orientados a eventos, seja respondendo a solicitações HTTP, manipulando carregamentos de arquivos no armazenamento de BLOBs ou processando eventos em uma fila.  Você escreve apenas o código necessário para lidar com seu evento sem se preocupar com servidores ou código de estrutura.  Além disso, você pode tirar proveito de mais de 250 conectores para outros serviços do Azure e de terceiros para lidar com seus problemas de integração mais difíceis.

## <a name="access-azure-services-from-net-applications"></a>Acessar serviços do Azure de aplicativos .NET

Se seu aplicativo está hospedado no Azure ou no local, o acesso à maioria dos serviços do Azure é fornecido por meio do **SDK do Azure para .net**.  O SDK do Azure para .NET é fornecido como uma série de pacotes NuGet e pode ser usado em aplicativos .NET Core (2,1 e superior) e .NET Framework (4.6.1 e superior). O SDK do Azure para .NET torna a incorporação de serviços do Azure em seu aplicativo tão fácil quanto a instalação do pacote NuGet correto, instanciando um objeto de cliente e chamando os métodos apropriados. Mais informações sobre o SDK do Azure para .NET podem ser encontradas na [visão geral do SDK do Azure para .net](./sdk/azure-sdk-for-dotnet.md).

![Diagrama mostrando como os aplicativos .NET usam o SDK do Azure para acessar os serviços do Azure](./media/azure-sdk-for-dotnet-overview.png)

## <a name="next-steps"></a>Próximas etapas

Em seguida, saiba mais sobre os [Serviços do Azure mais comumente usados](./key-azure-services.md) para o desenvolvimento do .net.
