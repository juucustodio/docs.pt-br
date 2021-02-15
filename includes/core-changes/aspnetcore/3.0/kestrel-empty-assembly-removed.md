---
ms.openlocfilehash: 1c9c899d77dd69e185281d98bfec18ce73d80815
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032253"
---
### <a name="kestrel-empty-https-assembly-removed"></a>Kestrel: assembly HTTPS vazio removido

O assembly foi <xref:Microsoft.AspNetCore.Server.Kestrel.Https?displayProperty=fullName> removido.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="reason-for-change"></a>Motivo da alteração

No ASP.NET Core 2,1, o conteúdo de `Microsoft.AspNetCore.Server.Kestrel.Https` foi movido para <xref:Microsoft.AspNetCore.Server.Kestrel.Core?displayProperty=fullName> . Essa alteração foi feita de forma não-significativa usando `[TypeForwardedTo]` atributos.

#### <a name="recommended-action"></a>Ação recomendada

- As bibliotecas `Microsoft.AspNetCore.Server.Kestrel.Https` que fazem referência a 2,0 devem atualizar todas as dependências de ASP.NET Core para 2,1 ou posterior. Caso contrário, eles poderão ser interrompidos quando forem carregados em um aplicativo ASP.NET Core 3,0.
- Os aplicativos e bibliotecas destinados a ASP.NET Core 2,1 e posterior devem remover todas as referências diretas ao `Microsoft.AspNetCore.Server.Kestrel.Https` pacote NuGet.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
