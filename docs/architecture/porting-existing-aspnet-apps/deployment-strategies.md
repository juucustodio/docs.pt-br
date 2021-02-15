---
title: Estratégias de implantação
description: Quais estratégias de implantação as equipes podem usar ao migrar do ASP.NET para o ASP.NET Core? Uma migração incremental pode permitir a implantação lado a lado de aplicativos .NET Framework e .NET Core, oferecendo uma experiência de usuário final tranqüila?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 85797ed0003e7dd2f53fad3b51876ae1cf01b0ba
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488392"
---
# <a name="deployment-strategies"></a>Estratégias de implantação

Uma consideração à medida que você planeja a migração de seu aplicativo ASP.NET grande para ASP.NET Core é como você implantará o novo aplicativo. Com o ASP.NET, as opções de implantação eram limitadas ao IIS no Windows. Com o ASP.NET Core, uma matriz muito mais ampla de opções de implantação está disponível.

## <a name="cross-platform-options"></a>Opções de plataforma cruzada

Como o .NET Core é executado no Linux, você encontrará algumas opções de hospedagem disponíveis que não eram consideradas anteriormente. A hospedagem baseada em Linux pode ser preferível pelos seguintes motivos:

* Sua organização tem infraestrutura ou experiência.
* Os provedores de hospedagem oferecem recursos atraentes ou preços para hospedagem baseada em Linux.

O .NET Core é aberto para portar a essas opções.

## <a name="cloud-native-development"></a>Desenvolvimento nativo de nuvem

A maioria das organizações atualmente está usando plataformas de nuvem para pelo menos alguns dos seus recursos de software. Com uma migração de aplicativo para o .NET Core, é um bom momento para considerar se o aplicativo deve ser intencionalmente escrito com a hospedagem na nuvem em mente. Esses aplicativos *nativos de nuvem* são mais capazes de aplicar recursos de nuvem, como sem servidor, de microatendimento, e podem ser menos preocupados com os detalhes de baixo nível de como e onde eles podem ser implantados.

Saiba mais sobre o desenvolvimento de aplicativos nativos de nuvem neste livro eletrônico gratuito, [Arquitetando aplicativos .net nativos de nuvem para o Azure](/dotnet/architecture/cloud-native/).

## <a name="leverage-containers"></a>Aproveitar contêineres

Aplicativos modernos geralmente aproveitam contêineres como um meio de reduzir a variação entre ambientes de hospedagem. Ao implantar um aplicativo em um contêiner específico, o aplicativo hospedado por contêiner será executado da mesma forma, seja em execução no laptop de um desenvolvedor ou em produção. Como parte de uma migração para o .NET Core, pode fazer sentido considerar se o aplicativo se beneficiaria da implantação por meio do contêiner, seja como um monolítico completo ou dividido em vários aplicativos em contêineres menores.

## <a name="side-by-side-deployment-options"></a>Opções de implantação lado a lado

A migração de grandes .NET Framework aplicativos para o .NET Core geralmente requer um esforço substancial. A maioria das organizações desejará poder dividir esse esforço de alguma forma, de modo que as partes do aplicativo possam ser migradas e implantadas em produção antes que toda a migração seja concluída. Executar o aplicativo ASP.NET original e seus subaplicativos ASP.NET Core recentemente migrados lado a lado é uma meta citada com frequência. Isso pode ser obtido por meio de vários mecanismos, incluindo o uso do roteamento do IIS, que é abordado no [capítulo 5](deployment-scenarios.md). Outras opções incluem o aproveitamento de gateways de aplicativo ou padrões de design de nuvem, como [back-ends para front-ends](https://docs.microsoft.com/azure/architecture/patterns/backends-for-frontends) , para gerenciar conjuntos de APIs Web ASP.net e pontos de extremidade de API de ASP.NET Core.

## <a name="iis-on-windows"></a>IIS no Windows

Você pode continuar hospedando seus aplicativos no IIS em execução no Windows. Essa é uma opção adequada para os clientes que desejam aproveitar os recursos de ASP.NET Core sem alterar seu modelo de implantação atual. Ao mover para ASP.NET Core fornece mais opções em termos de como e onde implantar seus aplicativos, não requer que você altere a partir do status quo do uso da combinação comprovada do IIS no Windows.

## <a name="other-options-on-windows"></a>Outras opções no Windows

Você pode hospedar aplicativos lado a lado no Windows usando qualquer combinação de hosts Kestrel, HTTP.sys e IIS, além de contêineres do Docker, se necessário. Se seu aplicativo exigir uma combinação de serviços do Windows e do Linux, hospedar um Windows Server com contêineres do [WSL](https://docs.microsoft.com/windows/wsl/about) e/ou Linux Docker fornecerá uma única solução de servidor para hospedar todas as partes do aplicativo.

## <a name="references"></a>Referências

- [Hospedar e implantar o ASP.NET Core](https://docs.microsoft.com/aspnet/core/host-and-deploy/)
- [Hospedar o ASP.NET Core no Windows com o IIS](https://docs.microsoft.com/aspnet/core/host-and-deploy/iis/)
- [Solução de problemas ASP.NET Core no serviço Azure App e no IIS](https://docs.microsoft.com/aspnet/core/test/troubleshoot-azure-iis)

>[!div class="step-by-step"]
>[Anterior](migrate-web-forms.md) 
> [Avançar](additional-migration-resources.md)
