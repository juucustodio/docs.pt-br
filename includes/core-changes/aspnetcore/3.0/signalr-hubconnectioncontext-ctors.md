---
ms.openlocfilehash: 6be98e7ced6608ba0793c635adfe61c8b1a7e9d9
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032308"
---
### <a name="signalr-hubconnectioncontext-constructors-changed"></a>Signalr: construtores HubConnectionContext alterados

Os construtores do signalr `HubConnectionContext` foram alterados para aceitar um tipo de opções, em vez de vários parâmetros, para a adição de opções à prova de futuro. Essa alteração substitui dois construtores por um único Construtor que aceita um tipo de opções.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

`HubConnectionContext` tem dois construtores:

```csharp
public HubConnectionContext(ConnectionContext connectionContext, TimeSpan keepAliveInterval, ILoggerFactory loggerFactory);
public HubConnectionContext(ConnectionContext connectionContext, TimeSpan keepAliveInterval, ILoggerFactory loggerFactory, TimeSpan clientTimeoutInterval);
```

#### <a name="new-behavior"></a>Novo comportamento

Os dois construtores foram removidos e substituídos por um construtor:

```csharp
public HubConnectionContext(ConnectionContext connectionContext, HubConnectionContextOptions contextOptions, ILoggerFactory loggerFactory)
```

#### <a name="reason-for-change"></a>Motivo da alteração

O novo construtor usa um novo objeto Options. Consequentemente, os recursos do `HubConnectionContext` podem ser expandidos no futuro sem necessidade de mais construtores nem de alterações interruptivas.

#### <a name="recommended-action"></a>Ação recomendada

Em vez de usar o Construtor a seguir:

```csharp
HubConnectionContext connectionContext = new HubConnectionContext(
    connectionContext,
    keepAliveInterval: TimeSpan.FromSeconds(15),
    loggerFactory,
    clientTimeoutInterval: TimeSpan.FromSeconds(15));
```

Use o seguinte construtor:

```csharp
HubConnectionContextOptions contextOptions = new HubConnectionContextOptions()
{
    KeepAliveInterval = TimeSpan.FromSeconds(15),
    ClientTimeoutInterval = TimeSpan.FromSeconds(15)
};
HubConnectionContext connectionContext = new HubConnectionContext(connectionContext, contextOptions, loggerFactory);
```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.SignalR.HubConnectionContext.%23ctor(Microsoft.AspNetCore.Connections.ConnectionContext,System.TimeSpan,Microsoft.Extensions.Logging.ILoggerFactory)>
- <xref:Microsoft.AspNetCore.SignalR.HubConnectionContext.%23ctor(Microsoft.AspNetCore.Connections.ConnectionContext,System.TimeSpan,Microsoft.Extensions.Logging.ILoggerFactory,System.TimeSpan)>

<!--

#### Affected APIs

- `M:Microsoft.AspNetCore.SignalR.HubConnectionContext.#ctor(Microsoft.AspNetCore.Connections.ConnectionContext,System.TimeSpan,Microsoft.Extensions.Logging.ILoggerFactory)`
- `M:Microsoft.AspNetCore.SignalR.HubConnectionContext.#ctor(Microsoft.AspNetCore.Connections.ConnectionContext,System.TimeSpan,Microsoft.Extensions.Logging.ILoggerFactory,System.TimeSpan)`

-->
