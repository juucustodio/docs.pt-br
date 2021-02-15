---
title: 'Alteração significativa: Kestrel: transporte Libuv marcado como obsoleto'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado Kestrel: transporte Libuv marcado como obsoleto'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: f66b9b646671e07957e6d30a95333d392eb29617
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760398"
---
# <a name="kestrel-libuv-transport-marked-as-obsolete"></a>Kestrel: transporte Libuv marcado como obsoleto

As versões anteriores do ASP.NET Core usavam Libuv como um detalhe de implementação de como a entrada e a saída assíncronas foram executadas. No ASP.NET Core 2,0, <xref:System.Net.Sockets.Socket> foi desenvolvido um transporte baseado em alternativa. No ASP.NET Core 2,1, o Kestrel mudou para usar o `Socket` transporte baseado por padrão. O suporte a Libuv foi mantido por motivos de compatibilidade.

Neste ponto, o uso do `Socket` transporte baseado é muito mais comum do que o transporte Libuv. Consequentemente, o suporte a Libuv é marcado como obsoleto no .NET 5,0 e será totalmente removido no .NET 6,0.

Como parte dessa alteração, o suporte do Libuv para novas plataformas de sistema operacional (como o Windows ARM64) não será adicionado no período de tempo do .NET 5,0.

Para obter uma discussão sobre problemas de bloqueio que exigem o uso do transporte Libuv, consulte o problema do GitHub em [dotnet/aspnetcore # 23409](https://github.com/dotnet/aspnetcore/issues/23409).

## <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

## <a name="old-behavior"></a>Comportamento antigo

As APIs Libuv não são marcadas como obsoletas.

## <a name="new-behavior"></a>Novo comportamento

As APIs Libuv são marcadas como obsoletas.

## <a name="reason-for-change"></a>Motivo da alteração

O `Socket` transporte baseado em é o padrão. Não há nenhum motivo convincente para continuar usando o transporte Libuv.

## <a name="recommended-action"></a>Ação recomendada

Descontinue o uso do [pacote Libuv](https://www.nuget.org/packages/Libuv) e dos métodos de extensão.

## <a name="affected-apis"></a>APIs afetadas

- [WebHostBuilderLibuvExtensions](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions?view=aspnetcore-3.0)
- [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. Transport. Libuv. LibuvTransportOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. Transport. Libuv. LibuvTransportOptions. ThreadCount](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.threadcount?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. Transport. Libuv. LibuvTransportOptions. NoDelay](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.nodelay?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. Transport. Libuv. LibuvTransportOptions. MaxWriteBufferSize](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.maxwritebuffersize?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. Transport. Libuv. LibuvTransportOptions. MaxReadBufferSize](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.maxreadbuffersize?view=aspnetcore-3.0)
- `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.Backlog`

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.AspNetCore.Hosting.WebHostBuilderLibuvExtensions`
- `Overload:Microsoft.AspNetCore.Hosting.WebHostBuilderLibuvExtensions.UseLibuv`
- `T:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.ThreadCount`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.NoDelay`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.MaxWriteBufferSize`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.MaxReadBufferSize`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.Backlog`

-->
