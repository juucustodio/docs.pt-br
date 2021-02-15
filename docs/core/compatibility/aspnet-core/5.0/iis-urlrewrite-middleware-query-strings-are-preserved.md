---
title: 'Alteração significativa: IIS: as cadeias de consulta de middleware UrlRewrite são preservadas'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado IIS: cadeias de consulta de middleware UrlRewrite são preservadas'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: e4d1ecba62f9e43e7377aba1138968f15f8895d5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760312"
---
# <a name="iis-urlrewrite-middleware-query-strings-are-preserved"></a>IIS: cadeias de consulta de middleware UrlRewrite são preservadas

Um defeito de middleware UrlRewrite do IIS impediu que a cadeia de caracteres de consulta fosse preservada nas regras de regravação. Esse defeito foi corrigido para manter a consistência com o comportamento do módulo UrlRewrite do IIS.

Para obter uma discussão, veja Issue [dotnet/aspnetcore # 22972](https://github.com/dotnet/aspnetcore/issues/22972).

## <a name="version-introduced"></a>Versão introduzida

ASP.NET Core 5,0 Preview 7

## <a name="old-behavior"></a>Comportamento antigo

Considere a seguinte regra de reescrita:

```xml
<rule name="MyRule" stopProcessing="true">
  <match url="^about" />
  <action type="Redirect" url="/contact" redirectType="Temporary" appendQueryString="true" />
</rule>
```

A regra anterior não acrescenta a cadeia de caracteres de consulta. Um URI como `/about?id=1` redireciona para `/contact` em vez de `/contact?id=1` . O `appendQueryString` atributo `true` também usa como padrão.

## <a name="new-behavior"></a>Novo comportamento

A cadeia de caracteres de consulta é preservada. O URI do exemplo no [comportamento antigo](#old-behavior) seria `/contact?id=1` .

## <a name="reason-for-change"></a>Motivo da alteração

O comportamento antigo não correspondia ao comportamento do módulo UrlRewrite do IIS. Para dar suporte à portabilidade entre o middleware e o módulo, o objetivo é manter comportamentos consistentes.

## <a name="recommended-action"></a>Ação recomendada

Se o comportamento de remover a cadeia de caracteres de consulta for preferencial, defina o `action` elemento como `appendQueryString="false"` .

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Rewrite.IISUrlRewriteOptionsExtensions.AddIISUrlRewrite%2A?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`Overload:Microsoft.AspNetCore.Rewrite.IISUrlRewriteOptionsExtensions.AddIISUrlRewrite`

-->
