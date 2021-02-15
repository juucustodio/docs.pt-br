---
ms.openlocfilehash: 9d138f79fcede4acac837f8d7793aa343ced737c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032243"
---
### <a name="http-defaulthttpcontext-extensibility-removed"></a>HTTP: extensibilidade defaulthttpcontext removida

Como parte dos aprimoramentos de desempenho do ASP.NET Core 3,0, a extensibilidade do `DefaultHttpContext` foi removida. A classe agora é `sealed` . Para obter mais informações, consulte [dotnet/aspnetcore # 6504](https://github.com/dotnet/aspnetcore/pull/6504).

Se os testes de unidade usarem `Mock<DefaultHttpContext>` , use `Mock<HttpContext>` ou `new DefaultHttpContext()` em vez disso.

Para obter uma discussão, consulte [dotnet/aspnetcore # 6534](https://github.com/dotnet/aspnetcore/issues/6534).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Classes podem derivar de `DefaultHttpContext` .

#### <a name="new-behavior"></a>Novo comportamento

Classes não podem derivar de `DefaultHttpContext` .

#### <a name="reason-for-change"></a>Motivo da alteração

A extensibilidade foi inicialmente fornecida para permitir o pooling do `HttpContext` , mas introduziu uma complexidade desnecessária e impedia outras otimizações.

#### <a name="recommended-action"></a>Ação recomendada

Se você estiver usando `Mock<DefaultHttpContext>` em seus testes de unidade, comece a usar `Mock<HttpContext>` em vez disso.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Http.DefaultHttpContext?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.Http.DefaultHttpContext`

-->
