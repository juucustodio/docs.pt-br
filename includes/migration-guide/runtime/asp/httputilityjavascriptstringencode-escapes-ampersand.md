---
ms.openlocfilehash: b648aee35ff44730f545f0fa06f4e0a86615dece
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606903"
---
### <a name="httputilityjavascriptstringencode-escapes-ampersand"></a>HttpUtility.JavaScriptStringEncode escapa o E comercial

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.5, <xref:System.Web.HttpUtility.JavaScriptStringEncode(System.String)?displayProperty=fullName> ignora o caractere E comercial (&amp;).

#### <a name="suggestion"></a>Sugestão

Se seu aplicativo depende do comportamento anterior desse método, você poderá adicionar uma definição aspnet:JavaScriptDoNotEncodeAmpersand ao [elemento appSettings do ASP.NET](/previous-versions/aspnet/hh975440(v=vs.120)) no seu arquivo de configuração.

| Name    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Web.HttpUtility.JavaScriptStringEncode(System.String)?displayProperty=nameWithType>
- <xref:System.Web.HttpUtility.JavaScriptStringEncode(System.String,System.Boolean)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Web.HttpUtility.JavaScriptStringEncode(System.String)`
- `M:System.Web.HttpUtility.JavaScriptStringEncode(System.String,System.Boolean)`

-->
