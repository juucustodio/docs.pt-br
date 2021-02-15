---
ms.openlocfilehash: b3cc04d5675ea63a0a6b967e293da8a1bd79830d
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031954"
---
### <a name="uribuilder-properties-no-longer-prepend-leading-characters"></a>As propriedades UriBuilder não precedem mais os caracteres à esquerda

<xref:System.UriBuilder.Fragment?displayProperty=nameWithType> Não precede mais um caractere à esquerda `#` e <xref:System.UriBuilder.Query?displayProperty=nameWithType> não precede mais um caractere à esquerda `?` quando já existe um.

#### <a name="change-description"></a>Descrição das alterações

Em .NET Framework, as <xref:System.UriBuilder.Fragment?displayProperty=nameWithType> <xref:System.UriBuilder.Query?displayProperty=nameWithType> Propriedades e sempre precedem um `#` `?` caractere ou, respectivamente, ao valor que está sendo armazenado. Esse comportamento pode resultar em vários `#` `?` caracteres ou no valor armazenado se a cadeia de caracteres já contiver um desses caracteres à esquerda. Por exemplo, o valor de <xref:System.UriBuilder.Fragment?displayProperty=nameWithType> pode se tornar `##main` .

A partir do .NET Core 1,0, essas propriedades não precedem mais os `#` `?` caracteres ou ao valor armazenado, se já houver um presente no início da cadeia de caracteres.

#### <a name="version-introduced"></a>Versão introduzida

1.0

#### <a name="recommended-action"></a>Ação recomendada

Você não precisa mais remover explicitamente nenhum desses caracteres à esquerda ao definir os valores de propriedade. Isso é especialmente útil quando você está acrescentando valores, porque você não precisa mais remover o à esquerda `#` ou `?` cada vez que você acrescenta.

Por exemplo, o trecho de código a seguir mostra a diferença de comportamento entre .NET Framework e o .NET Core.

```csharp
var builder = new UriBuilder();
builder.Query = "one=1";
builder.Query += "&two=2";
builder.Query += "&three=3";
builder.Query += "&four=4";

Console.WriteLine(builder.Query);
```

- Em .NET Framework, a saída é `????one=1&two=2&three=3&four=4` .
- No .NET Core, a saída é `?one=1&two=2&three=3&four=4` .

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.UriBuilder.Fragment?displayProperty=fullName>
- <xref:System.UriBuilder.Query?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.UriBuilder.Fragment`
- `T:System.UriBuilder.Query`

-->
