---
title: 'Alteração significativa: os tipos mais recentes: JSObjectReference e JSInProcessObjectReference foram alterados para interno'
description: 'Saiba mais sobre as alterações significativas no ASP.NET Core 5,0 intitulados mais recentes: JSObjectReference e JSInProcessObjectReference tipos alterados para interno'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 43a66d204f8309dc5afc57d099b2201c477cc3ad
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760379"
---
# <a name="blazor-jsobjectreference-and-jsinprocessobjectreference-types-changed-to-internal"></a>Mais de: JSObjectReference e tipos JSInProcessObjectReference alterados para interno

Os novos `Microsoft.JSInterop.JSObjectReference` e os `Microsoft.JSInterop.JSInProcessObjectReference` tipos introduzidos no ASP.NET Core 5,0 RC1 foram marcados como `internal` .

## <a name="version-introduced"></a>Versão introduzida

5,0 RC2

## <a name="old-behavior"></a>Comportamento antigo

Um `JSObjectReference` pode ser obtido de uma chamada de interoperabilidade JavaScript por meio do `IJSRuntime` . Por exemplo:

```csharp
var jsObjectReference = await JSRuntime.InvokeAsync<JSObjectReference>(...);
```

## <a name="new-behavior"></a>Novo comportamento

`JSObjectReference` usa o modificador de acesso [interno](../../../../csharp/language-reference/keywords/internal.md) . A `public` `IJSObjectReference` interface deve ser usada em seu lugar. Por exemplo:

```csharp
var jsObjectReference = await JSRuntime.InvokeAsync<IJSObjectReference>(...);
```

`JSInProcessObjectReference` também foi marcado como `internal` e foi substituído por `IJSInProcessObjectReference` .

## <a name="reason-for-change"></a>Motivo da alteração

A alteração torna o recurso de interoperabilidade JavaScript mais consistente com outros padrões no mais baixo. `IJSObjectReference` é análogo a `IJSRuntime` , pois ele atende a uma finalidade semelhante e tem métodos e extensões semelhantes.

## <a name="recommended-action"></a>Ação recomendada

Substituir ocorrências de `JSObjectReference` e `JSInProcessObjectReference` por `IJSObjectReference` e `IJSInProcessObjectReference` , respectivamente.

## <a name="affected-apis"></a>APIs afetadas

- `Microsoft.JSInterop.JSObjectReference`
- `Microsoft.JSInterop.JSInProcessObjectReference`

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.JSInterop.JSObjectReference`
- `T:Microsoft.JSInterop.JSInProcessObjectReference`

-->
