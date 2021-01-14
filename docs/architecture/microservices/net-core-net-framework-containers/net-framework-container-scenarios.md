---
title: Quando escolher o .NET Framework para os contêineres do Docker
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Quando escolher o .NET Framework para os contêineres do Docker
ms.date: 01/13/2021
ms.openlocfilehash: 476f891a70a220172f84d8168c8492416b8e56bd
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188109"
---
# <a name="when-to-choose-net-framework-for-docker-containers"></a>Quando escolher o .NET Framework para os contêineres do Docker

Embora o .NET 5 ofereça benefícios significativos para novos aplicativos e padrões de aplicativos, .NET Framework continuará a ser uma boa opção para muitos cenários existentes.

## <a name="migrating-existing-applications-directly-to-a-windows-server-container"></a>Migrando aplicativos existentes diretamente para um contêiner do Windows Server

Talvez convenha usar contêineres do Docker apenas para simplificar a implantação, mesmo se você não estiver criando microsserviços. Por exemplo, talvez convenha aprimorar seu fluxo de trabalho DevOps com o Docker — os contêineres podem oferecer ambientes de teste mais bem isolados e também podem eliminar problemas de implantação causados por dependências ausentes quando você muda para um ambiente de produção. Em casos assim, mesmo se você estiver implantando um aplicativo monolítico, faz sentido usar os contêineres do Docker e do Windows para seus aplicativos .NET Framework atuais.

Na maioria dos casos, para esse cenário, não será necessário migrar seus aplicativos existentes para o .NET 5; Você pode usar contêineres do Docker que incluem o .NET Framework tradicional. No entanto, uma abordagem recomendada é usar o .NET 5 à medida que você estende um aplicativo existente, como escrever um novo serviço no ASP.NET Core.

## <a name="using-third-party-net-libraries-or-nuget-packages-not-available-for-net-5"></a>Usando bibliotecas .NET de terceiros ou pacotes NuGet não disponíveis para o .NET 5

As bibliotecas de terceiros estão adotando rapidamente [.net Standard](../../../standard/net-standard.md), o que permite o compartilhamento de código em todos os tipos .net, incluindo o .NET 5. Com o .NET Standard 2,0 e posterior, a compatibilidade da superfície de API em diferentes estruturas se tornou significativamente maior. Ainda mais, o .NET Core 2. x e os aplicativos mais recentes também podem fazer referência direta a bibliotecas de .NET Framework existentes (Confira [.NET Framework 4.6.1 com suporte a .NET Standard 2,0](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#net-framework-461-supporting-net-standard-20)).

Além disso, o [pacote de compatibilidade do Windows](../../../core/porting/windows-compat-pack.md) estende a superfície de API disponível para .net Standard 2,0 no Windows. Este pacote permite recompilar a maioria do código existente para o .NET Standard 2.x com pouca ou nenhuma modificação para ser executado no Windows.

No entanto, mesmo com essa progressão excepcional desde .NET Standard 2,0 e o .NET Core 2,1 ou posterior, pode haver casos em que determinados pacotes NuGet precisam executar o Windows e talvez não ofereçam suporte ao .NET Core ou posterior. Se esses pacotes forem críticos ao aplicativo, será necessário usar o .NET Framework em contêineres do Windows.

## <a name="using-net-technologies-not-available-for-net-5"></a>Usando tecnologias .NET não disponíveis para o .NET 5

Algumas tecnologias .NET Framework não estão disponíveis na versão atual do .NET (versão 5,0 no momento da elaboração deste artigo). Alguns deles podem ser disponibilizados em versões posteriores, mas outros não se ajustam aos novos padrões de aplicativo destinados ao .NET Core e podem nunca estar disponíveis.

A lista a seguir mostra a maioria das tecnologias que não estão disponíveis no .NET 5:

- Web Forms do ASP.NET. Esta tecnologia só está disponível no .NET Framework. Atualmente, não há planos para trazer o ASP.NET Web Forms para o .NET ou posterior.

- Serviços WCF. Mesmo quando uma [biblioteca de cliente WCF](https://github.com/dotnet/wcf) está disponível para consumir serviços WCF do .NET 5, a partir de Jan-2021, a implementação do servidor WCF só está disponível no .NET Framework.

- Serviços relacionados a fluxo de trabalho. O Windows WF (Workflow Foundation), os Serviços de fluxo de trabalho (WCF + WF em um único serviço) e o WCF Data Services (anteriormente conhecido como Serviços de Dados ADO.NET) só estão disponíveis no .NET Framework. Atualmente, não há planos para trazê-los para o .NET 5.

Além das tecnologias listadas no roteiro oficial do [.net](https://github.com/dotnet/core/blob/master/roadmap.md), outros recursos podem ser portados para a nova [plataforma .net unificada](https://devblogs.microsoft.com/dotnet/introducing-net-5/). Você pode considerar participar das discussões no GitHub para que sua voz possa ser ouvida. E se você acreditar que algo está faltando, execute um novo problema no repositório do GitHub [dotnet/tempo de execução](https://github.com/dotnet/runtime/issues/new) .

## <a name="using-a-platform-or-api-that-doesnt-support-net-5"></a>Usando uma plataforma ou API que não dá suporte ao .NET 5

Algumas plataformas da Microsoft e de terceiros não oferecem suporte ao .NET 5. Por exemplo, alguns serviços do Azure fornecem um SDK que ainda não está disponível para consumo no .NET 5. A maioria dos SDK do Azure deve, eventualmente, ser portado para o .NET 5/Standard, mas alguns podem não por vários motivos. Você pode ver os SDKs do Azure disponíveis na página [versões mais recentes do SDK do Azure](https://azure.github.io/azure-sdk/releases/latest/index.html) .

Enquanto isso, se qualquer plataforma ou serviço no Azure ainda não oferecer suporte ao .NET 5 com sua API de cliente, você poderá usar a API REST equivalente do serviço do Azure ou do SDK do cliente no .NET Framework.

### <a name="additional-resources"></a>Recursos adicionais

- **Conceitos básicos do .NET** \
  [https://docs.microsoft.com/dotnet/fundamentals](../../../fundamentals/index.yml)

- **Portando projetos para o .NET 5** \
  [https://channel9.msdn.com/Events/dotnetConf/2020/Porting-Projects-to-NET-5](https://channel9.msdn.com/Events/dotnetConf/2020/Porting-Projects-to-NET-5)

- **.NET no guia do Docker** \
  [https://docs.microsoft.com/dotnet/core/docker/introduction](../../../core/docker/introduction.md)

- **Visão geral dos componentes .NET** \
  [https://docs.microsoft.com/dotnet/standard/components](../../../standard/components.md)

>[!div class="step-by-step"]
>[Anterior](net-core-container-scenarios.md) 
> [Avançar](container-framework-choice-factors.md)
