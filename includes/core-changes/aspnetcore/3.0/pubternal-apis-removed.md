---
ms.openlocfilehash: 224cd3c7897c64ef05baba7d3d31dbe5ac0dd610
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606765"
---
### <a name="pubternal-apis-removed"></a>APIs "Pubternal" removidas

Para manter a superfície da API pública de ASP.NET Core, a maioria dos tipos em `*.Internal` namespaces (conhecidos como :::no-loc text="\"pubternal\""::: APIs) se tornou verdadeiramente interna. Os membros desses namespaces nunca devem ter suporte como APIs voltadas para o público. As APIs podem ser interrompidas em versões secundárias e com frequência. O código que depende dessas APIs é interrompido ao atualizar para ASP.NET Core 3,0.

Para obter mais informações, consulte [dotnet/aspnetcore # 4932](https://github.com/dotnet/aspnetcore/issues/4932) e [dotnet/aspnetcore # 11312](https://github.com/dotnet/aspnetcore/issues/11312).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

As APIs afetadas são marcadas com o `public` modificador de acesso e existem em `*.Internal` namespaces.

#### <a name="new-behavior"></a>Novo comportamento

As APIs afetadas são marcadas com o modificador de acesso [interno](../../../../docs/csharp/language-reference/keywords/internal.md) e não podem mais ser usadas pelo código fora desse assembly.

#### <a name="reason-for-change"></a>Motivo da alteração

As diretrizes para essas :::no-loc text="\"pubternal\""::: APIs eram:

* Pode ser alterado sem aviso prévio.
* Não estavam sujeitas às políticas do .NET para evitar alterações interruptivas.

Deixar as APIs `public` (mesmo nos `*.Internal` namespaces) era confusa para os clientes.

#### <a name="recommended-action"></a>Ação recomendada

Pare de usar essas :::no-loc text="\"pubternal\""::: APIs. Se você tiver dúvidas sobre APIs alternativas, abra um problema no repositório [dotnet/aspnetcore](https://github.com/dotnet/aspnetcore/issues) .

Por exemplo, considere o seguinte código de buffer de solicitação HTTP em um projeto ASP.NET Core 2,2. O `EnableRewind` método de extensão existe no `Microsoft.AspNetCore.Http.Internal` namespace.

```csharp
HttpContext.Request.EnableRewind();
```

Em um projeto ASP.NET Core 3,0, substitua a `EnableRewind` chamada por uma chamada para o `EnableBuffering` método de extensão. O recurso de buffer de solicitação funciona como fazia no passado. `EnableBuffering` chama a `internal` API Now.

```csharp
HttpContext.Request.EnableBuffering();
```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Todas as APIs nos `Microsoft.AspNetCore.*` `Microsoft.Extensions.*` namespaces e que têm um `Internal` segmento no nome do namespace. Por exemplo:

- `Microsoft.AspNetCore.Authentication.Internal`
- `Microsoft.AspNetCore.Builder.Internal`
- `Microsoft.AspNetCore.DataProtection.Cng.Internal`
- `Microsoft.AspNetCore.DataProtection.Internal`
- `Microsoft.AspNetCore.Hosting.Internal`
- `Microsoft.AspNetCore.Http.Internal`
- `Microsoft.AspNetCore.Mvc.Core.Infrastructure`
- `Microsoft.AspNetCore.Mvc.Core.Internal`
- `Microsoft.AspNetCore.Mvc.Cors.Internal`
- `Microsoft.AspNetCore.Mvc.DataAnnotations.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Json.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Xml.Internal`
- `Microsoft.AspNetCore.Mvc.Internal`
- `Microsoft.AspNetCore.Mvc.ModelBinding.Internal`
- `Microsoft.AspNetCore.Mvc.Razor.Internal`
- `Microsoft.AspNetCore.Mvc.RazorPages.Internal`
- `Microsoft.AspNetCore.Mvc.TagHelpers.Internal`
- `Microsoft.AspNetCore.Mvc.ViewFeatures.Internal`
- `Microsoft.AspNetCore.Rewrite.Internal`
- `Microsoft.AspNetCore.Routing.Internal`
- `Microsoft.AspNetCore.Server.Kestrel.Core.Adapter.Internal`
- `Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http`
- `Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Infrastructure`
- `Microsoft.AspNetCore.Server.Kestrel.Https.Internal`

<!--

#### Affected APIs

- `N:Microsoft.AspNetCore.Authentication.Internal`
- `N:Microsoft.AspNetCore.Builder.Internal`
- `N:Microsoft.AspNetCore.DataProtection.Cng.Internal`
- `N:Microsoft.AspNetCore.DataProtection.Internal`
- `N:Microsoft.AspNetCore.Hosting.Internal`
- `N:Microsoft.AspNetCore.Http.Internal`
- `N:Microsoft.AspNetCore.Mvc.Core.Infrastructure`
- `N:Microsoft.AspNetCore.Mvc.Core.Internal`
- `N:Microsoft.AspNetCore.Mvc.Cors.Internal`
- `N:Microsoft.AspNetCore.Mvc.DataAnnotations.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Json.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Xml.Internal`
- `N:Microsoft.AspNetCore.Mvc.Internal`
- `N:Microsoft.AspNetCore.Mvc.ModelBinding.Internal`
- `N:Microsoft.AspNetCore.Mvc.Razor.Internal`
- `N:Microsoft.AspNetCore.Mvc.RazorPages.Internal`
- `N:Microsoft.AspNetCore.Mvc.TagHelpers.Internal`
- `N:Microsoft.AspNetCore.Mvc.ViewFeatures.Internal`
- `N:Microsoft.AspNetCore.Rewrite.Internal`
- `N:Microsoft.AspNetCore.Routing.Internal`
- `N:Microsoft.AspNetCore.Server.Kestrel.Core.Adapter.Internal`
- `N:Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http`
- `N:Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Infrastructure`
- `N:Microsoft.AspNetCore.Server.Kestrel.Https.Internal`

-->
