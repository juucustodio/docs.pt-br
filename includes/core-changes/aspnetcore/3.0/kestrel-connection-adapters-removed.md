---
ms.openlocfilehash: 06d5f48566c239e37355496c3f27163d952602c6
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032251"
---
### <a name="kestrel-connection-adapters-removed"></a>Kestrel: adaptadores de conexão removidos

Como parte da mudança para mover APIs "pubternal" para `public` o, o conceito de um `IConnectionAdapter` foi removido de Kestrel. Os adaptadores de conexão estão sendo substituídos pelo middleware de conexão (semelhante ao middleware HTTP no pipeline de ASP.NET Core, mas para conexões de nível inferior). O log de conexão e HTTPS foi movido dos adaptadores de conexão para o middleware de conexão. Esses métodos de extensão devem continuar funcionando sem problemas, mas os detalhes da implementação foram alterados.

Para obter mais informações, consulte [dotnet/aspnetcore # 11412](https://github.com/dotnet/aspnetcore/pull/11412). Para obter uma discussão, consulte [dotnet/aspnetcore # 11475](https://github.com/dotnet/aspnetcore/issues/11475).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Os componentes de extensibilidade do Kestrel foram criados usando o `IConnectionAdapter` .

#### <a name="new-behavior"></a>Novo comportamento

Os componentes de extensibilidade do Kestrel são criados como [middleware](https://github.com/dotnet/aspnetcore/pull/11412/files#diff-89acc06acf1b2e96bbdb811ce523619f).

#### <a name="reason-for-change"></a>Motivo da alteração

Essa alteração destina-se a fornecer uma arquitetura de extensibilidade mais flexível.

#### <a name="recommended-action"></a>Ação recomendada

Converta todas as implementações do `IConnectionAdapter` para usar o novo padrão de middleware, conforme mostrado [aqui](https://github.com/dotnet/aspnetcore/pull/11412/files#diff-89acc06acf1b2e96bbdb811ce523619f).

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

`Microsoft.AspNetCore.Server.Kestrel.Core.Adapter.Internal.IConnectionAdapter`

<!-- 

#### Affected APIs

`T:Microsoft.AspNetCore.Server.Kestrel.Core.Adapter.Internal.IConnectionAdapter`

-->
