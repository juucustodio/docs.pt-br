---
ms.openlocfilehash: 2a65caedea2af65796267aa145e275ebff814bf8
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032311"
---
### <a name="signalr-usesignalr-and-useconnections-methods-marked-obsolete"></a>Signalr: métodos UseSignalR e UseConnections marcados como obsoletos

Os métodos `UseConnections` e `UseSignalR` e as classes `ConnectionsRouteBuilder` e `HubRouteBuilder` são marcados como obsoletos no ASP.NET Core 3,0.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

O roteamento de Hub do signalr foi configurado usando o `UseSignalR` ou o `UseConnections` .

#### <a name="new-behavior"></a>Novo comportamento

A maneira antiga de configurar o roteamento foi obsoleta e substituída pelo roteamento de ponto de extremidade.

#### <a name="reason-for-change"></a>Motivo da alteração

O middleware está sendo movido para o novo sistema de roteamento de ponto de extremidade. A maneira antiga de adicionar o middleware está sendo obsoleta.

#### <a name="recommended-action"></a>Ação recomendada

Substituir `UseSignalR` por `UseEndpoints`:

**Código antigo:**

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<SomeHub>("/path");
});
```

**Novo código:**

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapHub<SomeHub>("/path");
});
```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.Builder.ConnectionsAppBuilderExtensions.UseConnections(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder})?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Builder.SignalRAppBuilderExtensions.UseSignalR(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.SignalR.HubRouteBuilder})?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.SignalR.HubRouteBuilder?displayProperty=fullName>

<!-- 

#### Affected APIs

- `M:Microsoft.AspNetCore.Builder.ConnectionsAppBuilderExtensions.UseConnections(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder})`
- `M:Microsoft.AspNetCore.Builder.SignalRAppBuilderExtensions.UseSignalR(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.SignalR.HubRouteBuilder})`
- `T:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder`
- `T:Microsoft.AspNetCore.SignalR.HubRouteBuilder`

-->
