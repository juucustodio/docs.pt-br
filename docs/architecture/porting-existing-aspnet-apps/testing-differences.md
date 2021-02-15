---
title: Compare as opções de teste entre o ASP.NET MVC e o ASP.NET Core
description: Como o teste é diferente entre os aplicativos ASP.NET MVC e os aplicativos ASP.NET Core?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 2821f97cf51fa5450c0cfae1287e845b6e19712d
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488430"
---
# <a name="compare-testing-options-between-aspnet-mvc-and-aspnet-core"></a>Compare as opções de teste entre o ASP.NET MVC e o ASP.NET Core

Os aplicativos ASP.NET MVC dão suporte ao teste de unidade de controladores, mas essa abordagem geralmente omite muitos recursos do MVC, como roteamento, autorização, associação de modelo, validação de modelo, filtros e muito mais. Para testar esses recursos do MVC além da lógica dentro da própria ação do controlador, muitas vezes o aplicativo precisaria ser implantado e testado com uma ferramenta como Selenium. Esses testes são substancialmente mais caros, mais frágeis e mais lentos que os testes de unidade típicos que podem ser executados sem a necessidade de hospedar e executar o aplicativo inteiro.

Os [controladores de ASP.NET Core podem ser testados em unidade](https://docs.microsoft.com/aspnet/core/mvc/controllers/testing) , assim como os controladores MVC ASP.net, mas com as mesmas limitações. No entanto, o [ASP.NET Core também dá suporte a testes de integração rápidos e fáceis de criar](https://docs.microsoft.com/aspnet/core/test/integration-tests) . Os testes de integração são hospedados por uma `TestHost` classe e normalmente são configurados em um personalizado `WebApplicationFactory` que pode substituir ou substituir dependências de aplicativo. Por exemplo, frequentemente durante os testes de integração, o aplicativo será direcionado a uma fonte de dados diferente e poderá substituir os serviços que enviam emails com implementações falsas ou fictícias.

O ASP.NET MVC e a API da Web não davam suporte a nada como os cenários de teste de integração disponíveis no ASP.NET Core. Em qualquer esforço de migração, você deve alocar tempo para escrever alguns testes de integração para seu sistema migrado recentemente para garantir que ele esteja funcionando conforme o esperado e continue a fazer isso. Mesmo que você não estivesse escrevendo testes de sua lógica do aplicativo Web antes da migração, deve ser altamente recomendável fazer isso ao mover para ASP.NET Core.

## <a name="references"></a>Referências

- [Criação de testes de unidade para aplicativos do ASP.NET MVC](https://docs.microsoft.com/aspnet/mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs)
- [Lógica do controlador de teste de unidade no ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/controllers/testing)
- [Testes de integração no ASP.NET Core](https://docs.microsoft.com/aspnet/core/test/integration-tests)

>[!div class="step-by-step"]
>[Anterior](signalr-differences.md) 
> [Avançar](migrate-large-solutions.md)
