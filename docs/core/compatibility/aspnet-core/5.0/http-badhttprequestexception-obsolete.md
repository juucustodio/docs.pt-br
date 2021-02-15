---
title: 'Alteração significativa: HTTP: Kestrel e tipos BadHttpRequestException do IIS marcados como obsoletos e substituídos'
description: 'Saiba mais sobre a alteração significativa em ASP.NET Core 5,0 intitulado HTTP: Kestrel e tipos BadHttpRequestException do IIS marcados como obsoletos e substituídos'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: c51b1dd9d708c04bc1bbcfb65ea2e9daea5330b4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760374"
---
# <a name="http-kestrel-and-iis-badhttprequestexception-types-marked-obsolete-and-replaced"></a>Tipos de BadHttpRequestException de HTTP: Kestrel e IIS marcados como obsoletos e substituídos

`Microsoft.AspNetCore.Server.Kestrel.BadHttpRequestException` e `Microsoft.AspNetCore.Server.IIS.BadHttpRequestException` foram marcados como obsoletos e alterados para derivar de `Microsoft.AspNetCore.Http.BadHttpRequestException` . Os servidores Kestrel e IIS ainda lançam seus tipos de exceção antigos para compatibilidade com versões anteriores. Os tipos obsoletos serão removidos em uma versão futura.

Para obter uma discussão, consulte [dotnet/aspnetcore # 20614](https://github.com/dotnet/aspnetcore/issues/20614).

## <a name="version-introduced"></a>Versão introduzida

5,0 versão prévia 4

## <a name="old-behavior"></a>Comportamento antigo

`Microsoft.AspNetCore.Server.Kestrel.BadHttpRequestException` e `Microsoft.AspNetCore.Server.IIS.BadHttpRequestException` derivado de <xref:System.IO.IOException?displayProperty=nameWithType> .

## <a name="new-behavior"></a>Novo comportamento

`Microsoft.AspNetCore.Server.Kestrel.BadHttpRequestException` e `Microsoft.AspNetCore.Server.IIS.BadHttpRequestException` são obsoletos. Os tipos também derivam de `Microsoft.AspNetCore.Http.BadHttpRequestException` , que deriva de `System.IO.IOException` .

## <a name="reason-for-change"></a>Motivo da alteração

A alteração foi feita em:

* Consolide tipos duplicados.
* Unificar o comportamento entre implementações do servidor.

Um aplicativo agora pode capturar a exceção base `Microsoft.AspNetCore.Http.BadHttpRequestException` ao usar o Kestrel ou o IIS.

## <a name="recommended-action"></a>Ação recomendada

Substitua os usos de `Microsoft.AspNetCore.Server.Kestrel.BadHttpRequestException` e `Microsoft.AspNetCore.Server.IIS.BadHttpRequestException` por `Microsoft.AspNetCore.Http.BadHttpRequestException` .

## <a name="affected-apis"></a>APIs afetadas

- [Microsoft. AspNetCore. Server. IIS. BadHttpRequestException](/dotnet/api/microsoft.aspnetcore.server.iis.badhttprequestexception?view=aspnetcore-3.1)
- [Microsoft. AspNetCore. Server. Kestrel. BadHttpRequestException](/dotnet/api/microsoft.aspnetcore.server.kestrel.badhttprequestexception?view=aspnetcore-1.1)

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.AspNetCore.Server.IIS.BadHttpRequestException`
- `T:Microsoft.AspNetCore.Server.Kestrel.BadHttpRequestException`

-->
