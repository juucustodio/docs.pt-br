---
ms.openlocfilehash: e5355387d5cb6d9e6de89f5b85e64bc100b32ae1
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032314"
---
### <a name="spas-spaservices-and-nodeservices-no-longer-fall-back-to-console-logger"></a>SPAs: SpaServices e Nodeservices não retornam mais para o agente do console

<xref:Microsoft.AspNetCore.SpaServices?displayProperty=nameWithType> e <xref:Microsoft.AspNetCore.NodeServices?displayProperty=nameWithType> não exibirá os logs do console, a menos que o log esteja configurado.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

`Microsoft.AspNetCore.SpaServices` e `Microsoft.AspNetCore.NodeServices` usado para criar automaticamente um agente de log do console quando o registro não estiver configurado.

#### <a name="new-behavior"></a>Novo comportamento

`Microsoft.AspNetCore.SpaServices` e `Microsoft.AspNetCore.NodeServices` não exibirá os logs do console, a menos que o log esteja configurado.

#### <a name="reason-for-change"></a>Motivo da alteração

Há a necessidade de se alinhar com o modo como outros pacotes de ASP.NET Core implementam o registro em log.

#### <a name="recommended-action"></a>Ação recomendada

Se o comportamento antigo for necessário, para configurar o log do console, adicione `services.AddLogging(builder => builder.AddConsole())` ao seu `Setup.ConfigureServices` método.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!--

#### Affected APIs

Not detectable via API analysis

-->
