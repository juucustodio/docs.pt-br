---
ms.openlocfilehash: be1fad236dd3eed047b010e93285aec8bc607b61
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032239"
---
### <a name="hosting-ihostingenvironment-and-iapplicationlifetime-types-marked-obsolete-and-replaced"></a>Hospedagem: tipos IHostingEnvironment e IApplicationLifetime marcados como obsoletos e substituídos

Novos tipos foram introduzidos para substituir os `IHostingEnvironment` tipos existentes e `IApplicationLifetime` .

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

Havia dois tipos diferentes `IHostingEnvironment` e `IApplicationLifetime` de `Microsoft.Extensions.Hosting` e `Microsoft.AspNetCore.Hosting` .

#### <a name="new-behavior"></a>Novo comportamento

Os tipos antigos foram marcados como obsoletos e substituídos por novos tipos.

#### <a name="reason-for-change"></a>Motivo da alteração

Quando `Microsoft.Extensions.Hosting` foi introduzido no ASP.NET Core 2,1, alguns tipos como `IHostingEnvironment` e `IApplicationLifetime` foram copiados de `Microsoft.AspNetCore.Hosting` . Algumas alterações ASP.NET Core 3,0 fazem com que os aplicativos incluam os `Microsoft.Extensions.Hosting` `Microsoft.AspNetCore.Hosting` namespaces e. Qualquer uso desses tipos duplicados causa um erro de compilador "referência ambígua" quando ambos os namespaces são referenciados.

#### <a name="recommended-action"></a>Ação recomendada

Substituídos os usos dos tipos antigos pelos tipos introduzidos recentemente, como abaixo:

**Tipos obsoletos (aviso):**

- <xref:Microsoft.Extensions.Hosting.IHostingEnvironment?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.EnvironmentName?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.EnvironmentName?displayProperty=nameWithType>

**Novos tipos:**

- <xref:Microsoft.Extensions.Hosting.IHostEnvironment?displayProperty=nameWithType>
- `Microsoft.AspNetCore.Hosting.IWebHostEnvironment : IHostEnvironment`
- <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.Environments?displayProperty=nameWithType>

Os `IHostEnvironment` `IsDevelopment` métodos New e `IsProduction` Extension estão no `Microsoft.Extensions.Hosting` namespace. Esse namespace pode precisar ser adicionado ao seu projeto.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.Hosting.EnvironmentName?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.EnvironmentName?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostingEnvironment?displayProperty=nameWithType>

<!-- 

#### Affected APIs

- `T:Microsoft.AspNetCore.Hosting.EnvironmentName`
- `T:Microsoft.AspNetCore.Hosting.IApplicationLifetime`
- `T:Microsoft.AspNetCore.Hosting.IHostingEnvironment`
- `T:Microsoft.Extensions.Hosting.EnvironmentName`
- `T:Microsoft.Extensions.Hosting.IApplicationLifetime`
- `T:Microsoft.Extensions.Hosting.IHostingEnvironment`

-->
