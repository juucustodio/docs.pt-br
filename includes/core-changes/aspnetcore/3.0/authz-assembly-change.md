---
ms.openlocfilehash: 2819fb3857fa6d40a2b2e42eeaec2d9c6e50eef0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96299347"
---
### <a name="authorization-addauthorization-overload-moved-to-different-assembly"></a>Autorização: sobrecarga de addautoria movida para um assembly diferente

Os `AddAuthorization` métodos principais que costumava residir em `Microsoft.AspNetCore.Authorization` foram renomeados para `AddAuthorizationCore` . Os `AddAuthorization` métodos antigos ainda existem, mas estão no `Microsoft.AspNetCore.Authorization.Policy` assembly em vez disso. Os aplicativos que usam os dois métodos não devem ter nenhum impacto. Observe que `Microsoft.AspNetCore.Authorization.Policy` agora é fornecido na estrutura compartilhada, em vez de um pacote autônomo, conforme discutido em [estrutura compartilhada: assemblies removidos do Microsoft. AspNetCore. app](#shared-framework-assemblies-removed-from-microsoftaspnetcoreapp).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

`AddAuthorization` os métodos existiam no `Microsoft.AspNetCore.Authorization` .

#### <a name="new-behavior"></a>Novo comportamento

`AddAuthorization` Existem métodos no `Microsoft.AspNetCore.Authorization.Policy` . `AddAuthorizationCore` é o novo nome para os métodos antigos.

#### <a name="reason-for-change"></a>Motivo da alteração

`AddAuthorization` é um nome de método melhor para adicionar todos os serviços comuns necessários para autorização.

#### <a name="recommended-action"></a>Ação recomendada

`Microsoft.AspNetCore.Authorization.Policy`Em vez disso, adicione uma referência a ou use `AddAuthorizationCore` .

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.Extensions.DependencyInjection.AuthorizationServiceCollectionExtensions.AddAuthorization(Microsoft.Extensions.DependencyInjection.IServiceCollection,System.Action{Microsoft.AspNetCore.Authorization.AuthorizationOptions})?displayProperty=fullName>

<!--

#### Affected APIs

`M:Microsoft.Extensions.DependencyInjection.AuthorizationServiceCollectionExtensions.AddAuthorization(Microsoft.Extensions.DependencyInjection.IServiceCollection,System.Action{Microsoft.AspNetCore.Authorization.AuthorizationOptions})`

-->
