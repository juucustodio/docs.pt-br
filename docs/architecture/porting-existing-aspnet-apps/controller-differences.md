---
title: Comparar controladores no ASP.NET MVC e ASP.NET Core
description: ASP.NET Core controladores MVC são semelhantes ao ASP.NET MVC 5 e aos controladores da API Web 2, mas há diferenças importantes. Esta seção examina as diferenças e as etapas necessárias para a porta de aplicativos do ASP.NET MVC e da API Web 2 para ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 7e5736f7a1ee5f33800fdf3a56f1aa4a8e40fb3a
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488403"
---
# <a name="compare-controllers-in-aspnet-mvc-and-web-api-with-controllers-in-aspnet-core"></a>Comparar controladores no ASP.NET MVC e na API Web com controladores no ASP.NET Core

No ASP.NET MVC 5 e na API da Web 2, havia dois `Controller` tipos base diferentes. Controladores MVC herdados de `Controller` ; Controladores de API Web herdados de `ApiController` . Em ASP.NET Core, essa hierarquia de objeto foi mesclada. É recomendável que os controladores de API no ASP.NET Core herdam de `ControllerBase` e adicionem o `[ApiController]` atributo. Os controladores MVC baseados em exibição padrão devem herdar de `Controller` .

Em ambas as estruturas, os controladores são usados para organizar conjuntos de métodos de ação. Filtros e rotas podem ser aplicados em um nível de controlador, além de no nível de ação. Essas convenções podem ser estendidas mais detalhadamente com o uso de tipos base personalizados `Controller` com comportamento padrão e atributos aplicados a eles.

No ASP.NET MVC, não há suporte para a negociação de conteúdo. O ASP.NET Web API 2 oferece suporte à negociação de conteúdo, assim como o ASP.NET Core. Usando a [negociação de conteúdo](https://docs.microsoft.com/aspnet/core/web-api/advanced/formatting), o formato do conteúdo retornado para uma solicitação pode ser determinado pelos cabeçalhos que o cliente fornece indicando sua maneira preferida de receber o conteúdo.

Ao migrar controladores ASP.NET Web API para ASP.NET Core, alguns componentes precisam ser alterados, se existirem. Isso inclui referências à `ApiController` classe base, ao `System.Web.Http` namespace e à `IHttpActionResult` interface. Consulte a [documentação para obter recomendações sobre como migrar essas diferenças específicas](https://docs.microsoft.com/aspnet/core/migration/webapi). Observe que o tipo de retorno preferencial para ações de API no ASP.NET Core é `ActionResult<T>` .

Além disso, o `[ChildActionOnly]` atributo não tem suporte no ASP.NET Core. No ASP.NET Core, uma funcionalidade semelhante é obtida usando [componentes de exibição](https://docs.microsoft.com/aspnet/core/mvc/views/view-components).

ASP.NET Core inclui dois novos atributos: [ConsumesAttribute](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.consumesattribute) e [produzattribute](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.producesattribute). Elas são usadas para especificar o tipo que uma ação consome ou produz, o que pode ser útil para rotear e documentar a API usando ferramentas como [Swagger/openapi](https://docs.microsoft.com/aspnet/core/tutorials/web-api-help-pages-using-swagger).

## <a name="references"></a>Referências

- [Formatar dados de resposta na API Web ASP.NET Core](https://docs.microsoft.com/aspnet/core/web-api/advanced/formatting)
- [Migrar de ASP.NET Web API para ASP.NET Core](https://docs.microsoft.com/aspnet/core/migration/webapi)

>[!div class="step-by-step"]
>[Anterior](identity-differences.md) 
> [Avançar](razor-differences.md)
