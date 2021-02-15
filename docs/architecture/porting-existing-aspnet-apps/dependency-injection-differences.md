---
title: Diferenças de injeção de dependência entre ASP.NET MVC e ASP.NET Core
description: Uma olhada em como a injeção de dependência funciona no ASP.NET MVC e ASP.NET Core, como eles diferem e como migrar do ASP.NET MVC para o ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 8d18486c7d0167c1e89bc9e5e822173f99c9985b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488398"
---
# <a name="dependency-injection-differences-between-aspnet-mvc-and-aspnet-core"></a>Diferenças de injeção de dependência entre ASP.NET MVC e ASP.NET Core

Embora a injeção de dependência (DI) não seja incorporada no MVC ou na API Web do ASP.NET, muitos aplicativos o habilitam adicionando um pacote NuGet com um contêiner inversão de controle (IOC). Às vezes, eles são chamados de contêineres de DI, para injeção de dependência (ou inversão). Alguns dos contêineres mais populares usados em aplicativos MVC do ASP.NET incluem:

- [Autofac](https://www.autofac.org/)
- [Unity](https://unitycontainer.github.io/)
- [Ninject](http://www.ninject.org/)
- [StructureMap](http://structuremap.github.io/) *(preterido)*
- [Castle Windsor](http://www.castleproject.org/projects/windsor/)

Se seu aplicativo ASP.NET MVC não estiver usando DI, provavelmente você desejará investigar o suporte interno para DI no ASP.NET Core. A DI promove o acoplamento flexível de módulos em seu aplicativo e permite melhor capacidade de teste e adesão a princípios como [sólidos](https://www.weeklydevtips.com/episodes/047).

Se seu aplicativo usa DI, provavelmente o melhor é que você veja se o contêiner que você está usando oferece suporte a ASP.NET Core. Nesse caso, você poderá continuar a usá-lo e suas regras de configuração personalizadas descrevendo os mapeamentos de tipo e os tempos de vida.

De qualquer forma, você deve considerar o uso do suporte interno para DI que acompanha o ASP.NET Core, pois ele pode atender às necessidades do seu aplicativo.

## <a name="dependency-injection-in-aspnet-core"></a>Injeção de dependência no ASP.NET Core

ASP.NET Core pressupõe que os aplicativos usarão DI. Ele não está apenas incorporado à estrutura, mas é necessário para dar suporte aos recursos de estrutura em seus aplicativos ASP.NET Core. Na inicialização do aplicativo, é feita uma chamada para a `ConfigureServices` qual é responsável pelo registro de todos os tipos que o contêiner de di (coleção de serviços/provedor de serviços) pode criar e injetar no aplicativo. Recursos internos de ASP.NET Core como Entity Framework Core, identidade e até MVC são trazidos para o aplicativo Configurando-os como serviços no `ConfigureServices` método.

Além de usar a implementação padrão, os aplicativos ainda podem usar contêineres personalizados. A [documentação aborda como substituir o contêiner de serviço padrão](https://docs.microsoft.com/dotnet/core/extensions/dependency-injection-guidelines#default-service-container-replacement).

DI é fundamental para ASP.NET Core. Se sua equipe ainda não estiver bem inválida nesta prática, você desejará compreender antes de portar seu aplicativo.

## <a name="references"></a>Referências

- [Injeção de dependência no .NET](https://docs.microsoft.com/dotnet/core/extensions/dependency-injection)
- [Injeção de dependência no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection)

>[!div class="step-by-step"]
>[Anterior](serving-static-files.md) 
> [Avançar](middleware-modules-handlers.md)
