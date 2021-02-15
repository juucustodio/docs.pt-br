---
title: 'Alteração significativa: autorização: o recurso no roteamento de ponto de extremidade é HttpContext'
description: 'Saiba mais sobre a alteração significativa na 5,0 ASP.NET Core a autorização intitulada: o recurso no roteamento do ponto de extremidade é HttpContext'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 7c5a77cb8999c60a7780b9b4f7ad2a1c79fd8310
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760524"
---
# <a name="authorization-resource-in-endpoint-routing-is-httpcontext"></a>Autorização: o recurso no roteamento de ponto de extremidade é HttpContext

Ao usar o roteamento de ponto de extremidade no ASP.NET Core 3,1, o recurso usado para autorização é o ponto de extremidade. Essa abordagem não era suficiente para obter acesso aos dados da rota ( <xref:Microsoft.AspNetCore.Routing.RouteData> ). Anteriormente no MVC, um <xref:Microsoft.AspNetCore.Http.HttpContext> recurso foi passado, o que permite o acesso ao ponto de extremidade ( <xref:Microsoft.AspNetCore.Http.Endpoint> ) e aos dados de rota. Essa alteração garante que o recurso passado para autorização seja sempre o `HttpContext` .

## <a name="version-introduced"></a>Versão introduzida

5,0 Preview 7

## <a name="old-behavior"></a>Comportamento antigo

Ao usar o roteamento de ponto de extremidade e os atributos de middleware de autorização ( <xref:Microsoft.AspNetCore.Authorization.AuthorizationMiddleware> ) ou [[autorizar]](xref:Microsoft.AspNetCore.Authorization.AuthorizeAttribute) , o recurso passado para autorização é o ponto de extremidade correspondente.

## <a name="new-behavior"></a>Novo comportamento

O roteamento do ponto de extremidade passa a `HttpContext` para a autorização.

## <a name="reason-for-change"></a>Motivo da alteração

Você pode acessar o ponto de extremidade do `HttpContext` . No entanto, não havia como ir do ponto de extremidade para coisas como os dados de rota. Houve uma perda na funcionalidade do roteamento sem ponto de extremidade.

## <a name="recommended-action"></a>Ação recomendada

Se seu aplicativo usar o recurso de ponto de extremidade, chame <xref:Microsoft.AspNetCore.Http.EndpointHttpContextExtensions.GetEndpoint%2A> no `HttpContext` para continuar acessando o ponto de extremidade.

No ASP.NET Core 5,0 Preview 8 e posterior, você pode reverter para o comportamento antigo com o <xref:System.AppContext.SetSwitch%2A> . Por exemplo:

```csharp
AppContext.SetSwitch(
    "Microsoft.AspNetCore.Authorization.SuppressUseHttpContextAsAuthorizationResource",
    isEnabled: true);
```

## <a name="affected-apis"></a>APIs afetadas

Nenhum

<!--

### Category

ASP.NET Core

### Affected APIs

Not detectable via API analysis

-->
