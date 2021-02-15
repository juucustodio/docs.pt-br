---
title: Comparar ASP.NET Web API 2 e ASP.NET Core
description: Como as APIs da Web diferem entre ASP.NET Web API 2 aplicativos e ASP.NET Core aplicativos?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 02e243591c0a6815cfe8371fbbc0b45a1cf22651
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488428"
---
# <a name="compare-aspnet-web-api-2-and-aspnet-core"></a>Comparar ASP.NET Web API 2 e ASP.NET Core

O ASP.NET Core oferece melhorias iterativas ao ASP.NET Web API 2, mas deve se familiarizar com os desenvolvedores que usaram a API Web 2. ASP.NET Web API 2 foi desenvolvido e enviado junto com o ASP.NET MVC. Isso significava que as duas abordagens tinham abordagens semelhantes, mas diferentes, para coisas como roteamento de atributos e injeção de dependência. No ASP.NET Core, não há mais nenhuma distinção entre o MVC e as APIs da Web. Há apenas ASP.NET MVC, que inclui suporte para cenários baseados em exibição, pontos de extremidade de API e Razor Pages (e outras variações, como o Signalr e verificações de integridade).

Além de ser consistente e unificado em ASP.NET Core, as APIs criadas no .NET Core são muito mais fáceis de testar do que aquelas criadas no ASP.NET Web API 2. Abordaremos as [diferenças de teste](testing-differences.md) em mais detalhes em alguns instantes. O suporte interno para hospedar aplicativos ASP.NET Core, em um host de teste que pode criar um `HttpClient` que faça solicitações na memória para o aplicativo, é um grande benefício quando se trata de testes automatizados.

Ao migrar do ASP.NET Web API 2 para ASP.NET Core, a transição é simples. Se você tiver controladores grandes e inflados, uma abordagem que você pode considerar para dividi-los é o uso dos pacotes NuGet [Ardalis. ApiEndpoints](https://www.nuget.org/packages/Ardalis.ApiEndpoints/) . Esse pacote divide cada ponto de extremidade em sua própria classe específica, com os tipos de solicitação e resposta associados, conforme apropriado. Essa abordagem gera muitos dos [mesmos benefícios que Razor Pages oferecem sobre a organização de código baseada em exibição](comparing-razor-pages-aspnet-mvc.md).

## <a name="references"></a>Referências

- [Migrar de ASP.NET Web API para ASP.NET Core](https://docs.microsoft.com/aspnet/core/migration/webapi)
- [Pacote NuGet Ardalis. ApiEndpoints](https://www.nuget.org/packages/Ardalis.ApiEndpoints/)

>[!div class="step-by-step"]
>[Anterior](comparing-razor-pages-aspnet-mvc.md) 
> [Avançar](authentication-differences.md)
