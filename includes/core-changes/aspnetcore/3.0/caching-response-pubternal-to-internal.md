---
ms.openlocfilehash: ae5a5fbf97ed4a03de7d35b9d5d5ca8de3aebc39
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032228"
---
### <a name="caching-responsecaching-pubternal-types-changed-to-internal"></a>Caching: tipos de ResponseCaching "pubternal" alterados para interno

No ASP.NET Core 3,0, os tipos "pubternal" no `ResponseCaching` foram alterados para `internal` .

Além disso, as implementações padrão do `IResponseCachingPolicyProvider` e do `IResponseCachingKeyProvider` não são mais adicionadas aos serviços como parte do `AddResponseCaching` método.

#### <a name="change-description"></a>Descrição das alterações

Em ASP.NET Core, os tipos "pubternal" são declarados como `public` , mas residem em um namespace com sufixo `.Internal` . Embora esses tipos sejam públicos, eles não têm nenhuma política de suporte e estão sujeitos a alterações interruptivas. O uso acidental desses tipos tem sido comum, resultando em alterações interruptivas nesses projetos e limitando a capacidade de manutenção da estrutura.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Esses tipos foram publicamente visíveis, mas sem suporte.

#### <a name="new-behavior"></a>Novo comportamento

Esses tipos agora são `internal` .

#### <a name="reason-for-change"></a>Motivo da alteração

O `internal` escopo reflete melhor a política sem suporte.

#### <a name="recommended-action"></a>Ação recomendada

Tipos de cópia que são usados pelo seu aplicativo ou biblioteca.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- `Microsoft.AspNetCore.ResponseCaching.Internal.CachedResponse`
- `Microsoft.AspNetCore.ResponseCaching.Internal.CachedVaryByRules`
- `Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCache`
- `Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCacheEntry`
- `Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingKeyProvider`
- `Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingPolicyProvider`
- `Microsoft.AspNetCore.ResponseCaching.Internal.MemoryResponseCache`
- `Microsoft.AspNetCore.ResponseCaching.Internal.ResponseCachingContext`
- `Microsoft.AspNetCore.ResponseCaching.Internal.ResponseCachingKeyProvider`
- `Microsoft.AspNetCore.ResponseCaching.Internal.ResponseCachingPolicyProvider`
- <xref:Microsoft.AspNetCore.ResponseCaching.ResponseCachingMiddleware.%23ctor(Microsoft.AspNetCore.Http.RequestDelegate,Microsoft.Extensions.Options.IOptions{Microsoft.AspNetCore.ResponseCaching.ResponseCachingOptions},Microsoft.Extensions.Logging.ILoggerFactory,Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingPolicyProvider,Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCache,Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingKeyProvider)?displayProperty=fullName>

<!-- 

#### Affected APIs

- `T:Microsoft.AspNetCore.ResponseCaching.Internal.CachedResponse`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.CachedVaryByRules`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCache`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCacheEntry`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingKeyProvider`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingPolicyProvider`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.MemoryResponseCache`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.ResponseCachingContext`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.ResponseCachingKeyProvider`
- `T:Microsoft.AspNetCore.ResponseCaching.Internal.ResponseCachingPolicyProvider`
- `M:Microsoft.AspNetCore.ResponseCaching.ResponseCachingMiddleware.#ctor(Microsoft.AspNetCore.Http.RequestDelegate,Microsoft.Extensions.Options.IOptions{Microsoft.AspNetCore.ResponseCaching.ResponseCachingOptions},Microsoft.Extensions.Logging.ILoggerFactory,Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingPolicyProvider,Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCache,Microsoft.AspNetCore.ResponseCaching.Internal.IResponseCachingKeyProvider)",
"nameWithType": "ResponseCachingMiddleware.ResponseCachingMiddleware(RequestDelegate, IOptions<ResponseCachingOptions>, ILoggerFactory, IResponseCachingPolicyProvider, IResponseCache, IResponseCachingKeyProvider)`

-->
