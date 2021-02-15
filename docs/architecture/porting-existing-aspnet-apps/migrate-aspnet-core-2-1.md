---
title: Migrar para o ASP.NET Core 2,1
description: Como a última versão do .NET Core para dar suporte ao direcionamento .NET Framework tempo de execução, a migração para o .NET Core 2,1 faz sentido como uma etapa intermediária em alguns planos de migração de aplicativo?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: a76b094d16ba4d1af057812335dc681a639f3a50
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488486"
---
# <a name="migrate-to-aspnet-core-21"></a>Migrar para o ASP.NET Core 2,1

ASP.NET Core 2,1 é uma versão interessante porque é a única versão do .NET Core com suporte no momento para dar suporte a tempos de execução do .NET Core e .NET Framework. Como tal, ele pode oferecer um caminho de atualização mais fácil para alguns aplicativos quando comparado à atualização de todas as partes do aplicativo para o .NET Core de uma só vez. Como uma versão LTS, o suporte para .NET Core 2,1 continuará até 2021 de agosto. O suporte para ASP.NET Core 2,1 em execução no .NET Framework continuará enquanto o .NET Framework subjacente for suportado.

## <a name="should-apps-run-on-net-framework-with-aspnet-core-21"></a>Os aplicativos devem ser executados em .NET Framework com ASP.NET Core 2,1?

ASP.NET Core 2,2 e versões anteriores suportavam os tempos de execução do .NET Core e do .NET Framework. Faz sentido migrar alguns ou todos os aplicativos para ASP.NET Core 2,1 como uma pedra de revisão, antes de portar completamente para o .NET Core? Aplicativos, ou subconjuntos de aplicativos, podem ver sua lógica ASP.NET de front-end portada para usar ASP.NET Core, ao mesmo tempo que ainda consome bibliotecas de .NET Framework para a lógica de negócios e o consumo de infraestrutura. Essa abordagem pode fazer sentido quando há uma camada de interface do usuário relativamente fina sem muita lógica de negócios e um conjunto muito maior de funcionalidade em bibliotecas de classes.

O principal benefício de portar apenas a camada da Web de front-end para ASP.NET Core 2,1 é que as bibliotecas de classes existentes do .NET podem permanecer como estão durante a migração inicial. Eles podem estar em uso contínuo por outros aplicativos .NET ou simplesmente não precisam estar no escopo da primeira iteração de uma migração completa planejada para o .NET Core. Reduzir o escopo da migração inicial para aplicativos grandes ajuda a fornecer metas incrementais que atuam como etapas de depuração em direção ao estado final desejado, que geralmente é uma porta completa para o .NET Core.

Se você tiver um aplicativo existente que possa usar essa estratégia, algumas coisas que você pode fazer hoje para ajudar a se preparar para o processo são mover o máximo possível de lógica de negócios, acesso a dados e outras lógicas sem interface do usuário dos projetos ASP.NET e de bibliotecas de classes separadas. Ele também ajudará se você tiver uma cobertura de teste automatizada do seu sistema, para que você possa verificar se o comportamento permanece consistente antes e depois da migração.

Se seu aplicativo é tão grande que você não pode migrar todo o aplicativo Web de uma vez e você precisa ser capaz de implantar o novo aplicativo ASP.NET Core lado a lado com o aplicativo ASP.NET existente, há estratégias de implantação que podem ser usadas para conseguir isso. Eles são abordados no [capítulo 5: cenários de implantação](deployment-scenarios.md).

Tenha em mente que ASP.NET Core 2,1 é a última versão LTS do .NET Core que dá suporte à execução em .NET Framework e consumo de bibliotecas de .NET Framework. Em breve, esta versão não terá suporte, mas ASP.NET Core 2,1 em .NET Framework terá suporte, desde que o .NET Framework (mesmo depois que o suporte do .NET Core 2,1 for encerrado). Para obter mais informações, consulte [ASP.NET Core 2,1 em .NET Framework](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).

## <a name="references"></a>Referências

[Migrando do ASP.NET para o ASP.NET Core 2,1](https://docs.microsoft.com/aspnet/core/migration/proper-to-2x/?view=aspnetcore-2.1&preserve-view=true)

>[!div class="step-by-step"]
>[Anterior](migration-considerations.md) 
> [Avançar](choose-net-core-version.md)
