---
ms.openlocfilehash: 96c2a32dd7cca91e965601d715bbd4625bba439a
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032298"
---
### <a name="mvc-jsonresult-moved-to-microsoftaspnetcoremvccore"></a>MVC: JsonResult movido para Microsoft. AspNetCore. Mvc. Core

`JsonResult` foi movido para o `Microsoft.AspNetCore.Mvc.Core` assembly. Esse tipo costumava ser definido no [Microsoft.AspNetCore.Mvc.Formatters.Jsem](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Formatters.Json). Um atributo de nível de assembly [[TypeForwardedTo]](xref:System.Runtime.CompilerServices.TypeForwardedToAttribute) foi adicionado ao `Microsoft.AspNetCore.Mvc.Formatters.Json` para resolver esse problema para a maioria dos usuários. Aplicativos que usam bibliotecas de terceiros podem encontrar problemas.

#### <a name="version-introduced"></a>Versão introduzida

3,0 Preview 6

#### <a name="old-behavior"></a>Comportamento antigo

Um aplicativo que usa uma biblioteca baseada em 2,2 é compilado com êxito.

#### <a name="new-behavior"></a>Novo comportamento

Um aplicativo que usa uma biblioteca com base em 2,2 falha na compilação. Um erro contendo uma variação do texto a seguir é fornecido:

```output
The type 'JsonResult' exists in both 'Microsoft.AspNetCore.Mvc.Core, Version=3.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60' and 'Microsoft.AspNetCore.Mvc.Formatters.Json, Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'
```

Para obter um exemplo desse problema, consulte [dotnet/aspnetcore # 7220](https://github.com/dotnet/aspnetcore/issues/7220).

#### <a name="reason-for-change"></a>Motivo da alteração

Alterações no nível da plataforma para a composição de ASP.NET Core conforme descrito em [ASPNET/comunicados # 325](https://github.com/aspnet/Announcements/issues/325).

#### <a name="recommended-action"></a>Ação recomendada

Bibliotecas compiladas com base na versão 2,2 do `Microsoft.AspNetCore.Mvc.Formatters.Json` talvez precisem ser recompiladas para resolver o problema de todos os consumidores. Se for afetado, contate o autor da biblioteca. Solicite a recompilação da biblioteca para o destino ASP.NET Core 3,0.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Mvc.JsonResult?displayProperty=nameWithType>

<!-- 

#### Affected APIs

`T:Microsoft.AspNetCore.Mvc.JsonResult`

-->
