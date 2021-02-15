---
ms.openlocfilehash: fb23418816abcae125106c93b339a546aa9bc2ee
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032252"
---
### <a name="kestrel-transport-abstractions-removed-and-made-public"></a>Kestrel: abstrações de transporte removidas e tornadas públicas

Como parte da afastamento das APIs "pubternal", as APIs da camada de transporte do Kestrel são expostas como uma interface pública na `Microsoft.AspNetCore.Connections.Abstractions` biblioteca.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

- Abstrações relacionadas ao transporte estavam disponíveis na `Microsoft.AspNetCore.Server.Kestrel.Transport.Abstractions` biblioteca.
- A `ListenOptions.NoDelay` Propriedade estava disponível.

#### <a name="new-behavior"></a>Novo comportamento

- A `IConnectionListener` interface foi introduzida na `Microsoft.AspNetCore.Connections.Abstractions` biblioteca para expor a funcionalidade mais usada da `...Transport.Abstractions` biblioteca.
- O `NoDelay` agora está disponível em opções de transporte ( `LibuvTransportOptions` e `SocketTransportOptions` ).
- `SchedulingMode` Não está mais disponível.

#### <a name="reason-for-change"></a>Motivo da alteração

ASP.NET Core 3,0 foi afastado das APIs "pubternal".

#### <a name="recommended-action"></a>Ação recomendada

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
