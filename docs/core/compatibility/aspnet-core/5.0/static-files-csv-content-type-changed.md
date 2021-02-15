---
title: 'Alteração significativa: arquivos estáticos: tipo de conteúdo CSV alterado para compatível com padrões'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado arquivos estáticos: tipo de conteúdo CSV alterado para compatível com padrões'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: c94a0cf213970d20559b7c061d8be220b43961e0
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760540"
---
# <a name="static-files-csv-content-type-changed-to-standards-compliant"></a>Arquivos estáticos: tipo de conteúdo CSV alterado para compatível com padrões

No ASP.NET Core 5,0, o `Content-Type` valor de cabeçalho de resposta padrão que o middleware de [arquivo estático](/aspnet/core/fundamentals/static-files) usa para arquivos *. csv* foi alterado para o valor em conformidade com os padrões `text/csv` .

Para obter uma discussão sobre esse problema, consulte [dotnet/aspnetcore # 17385](https://github.com/dotnet/AspNetCore/issues/17385).

## <a name="version-introduced"></a>Versão introduzida

5,0 visualização 1

## <a name="old-behavior"></a>Comportamento antigo

O `Content-Type` valor do cabeçalho `application/octet-stream` foi usado.

## <a name="new-behavior"></a>Novo comportamento

O `Content-Type` valor do cabeçalho `text/csv` é usado.

## <a name="reason-for-change"></a>Motivo da alteração

Conformidade com o padrão [RFC 7111](https://tools.ietf.org/html/rfc7111#section-5.1) .

## <a name="recommended-action"></a>Ação recomendada

Se essa alteração impactar seu aplicativo, você poderá personalizar o mapeamento de tipo de extensão para MIME do arquivo. Para reverter para o `application/octet-stream` tipo MIME, modifique a <xref:Microsoft.AspNetCore.Builder.StaticFileExtensions.UseStaticFiles%2A> chamada do método em `Startup.Configure` . Por exemplo:

```csharp
var provider = new FileExtensionContentTypeProvider();
provider.Mappings[".csv"] = MediaTypeNames.Application.Octet;

app.UseStaticFiles(new StaticFileOptions
{
    ContentTypeProvider = provider
});
```

Para obter mais informações sobre como personalizar o mapeamento, consulte [FileExtensionContentTypeProvider](/aspnet/core/fundamentals/static-files#fileextensioncontenttypeprovider).

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.StaticFiles.FileExtensionContentTypeProvider?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`T:Microsoft.AspNetCore.StaticFiles.FileExtensionContentTypeProvider`

-->
