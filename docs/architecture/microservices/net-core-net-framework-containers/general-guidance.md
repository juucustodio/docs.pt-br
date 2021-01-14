---
title: Orientação geral
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Diretrizes gerais
ms.date: 01/13/2021
ms.openlocfilehash: 4fd2d936c524cb3e5ae463038eaffe88b459d2bd
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98187945"
---
# <a name="general-guidance"></a>Orientação geral

Esta seção fornece um resumo de quando escolher o .NET 5 ou .NET Framework. Fornecemos mais detalhes sobre essas opções nas seções a seguir.

Use o .NET 5, com contêineres do Linux ou do Windows, para seu aplicativo de servidor Docker em contêiner quando:

- Você tiver necessidades de plataforma cruzada. Por exemplo, você desejar usar contêineres Linux e do Windows.

- Sua arquitetura de aplicativo for baseada em microsserviços.

- For necessário iniciar contêineres rapidamente e você desejar ocupar um espaço menor por contêiner para obter melhor densidade ou mais contêineres por unidade de hardware a fim de reduzir seus custos.

Em suma, ao criar novos aplicativos .NET em contêineres, você deve considerar o .NET 5 como a opção padrão. Ela tem muitos benefícios e se ajusta melhor à filosofia e ao estilo de trabalho dos contêineres.

Um benefício extra de usar o .NET 5 é que você pode executar versões do .NET lado a lado para aplicativos no mesmo computador. Esse benefício é mais importante para servidores ou VMs que não usam contêineres, porque os contêineres isolam as versões do .NET de que o aplicativo precisa. (Desde que sejam compatíveis com o sistema operacional subjacente.)

Use .NET Framework para seu aplicativo de servidor Docker em contêiner quando:

- No momento, seu aplicativo usar o .NET Framework e tem fortes dependências no Windows.

- Você precisa usar APIs do Windows que não têm suporte do .NET 5.

- Você precisa usar bibliotecas .NET de terceiros ou pacotes NuGet que não estão disponíveis para o .NET 5.

Usar o .NET Framework no Docker pode melhorar suas experiências de implantação minimizando os problemas de implantação. Este [cenário de "lift-and-shift"](https://aka.ms/liftandshiftwithcontainersebook) é importante para colocar aplicativos herdados em contêineres que foram desenvolvidos originalmente com o .NET Framework tradicional, como os serviços ASP.NET WebForms, aplicativos Web MVC ou WCF (Windows Communication Foundation).

### <a name="additional-resources"></a>Recursos adicionais

- **Livro eletrônico: modernizar os aplicativos .NET Framework existentes com contêineres do Azure e do Windows**  
    <https://aka.ms/liftandshiftwithcontainersebook>

- **Aplicativos de exemplo: modernização de aplicativos Web ASP.NET herdados usando Contêineres do Windows**  
    <https://aka.ms/eshopmodernizing>

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](net-core-container-scenarios.md)
