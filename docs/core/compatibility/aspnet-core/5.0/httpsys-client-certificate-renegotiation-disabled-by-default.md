---
title: 'Alteração significativa: HttpS: renegociação de certificado de cliente desabilitada por padrão'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado HttpS: renegociação de certificado de cliente desabilitada por padrão'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 796989e1a21e3cb206d081e4fe8f79630121dc84
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760313"
---
# <a name="httpsys-client-certificate-renegotiation-disabled-by-default"></a>HttpS: renegociação de certificado de cliente desabilitada por padrão

A opção para renegociar uma conexão e solicitar um certificado de cliente foi desabilitada por padrão. Para obter uma discussão, veja Issue [dotnet/aspnetcore # 23181](https://github.com/dotnet/aspnetcore/issues/23181).

## <a name="version-introduced"></a>Versão introduzida

ASP.NET Core 5,0

## <a name="old-behavior"></a>Comportamento antigo

A conexão pode ser renegociada para solicitar um certificado de cliente.

## <a name="new-behavior"></a>Novo comportamento

Certificados de cliente só podem ser solicitados durante o handshake de conexão inicial. Para obter mais informações, consulte solicitação pull [dotnet/aspnetcore # 23162](https://github.com/dotnet/aspnetcore/pull/23162).

## <a name="reason-for-change"></a>Motivo da alteração

A renegociação causou um número de problemas de desempenho e deadlock. Também não tem suporte no HTTP/2. Para obter o contexto adicional de quando a opção para controlar esse comportamento foi introduzida no ASP.NET Core 3,1, veja o problema [dotnet/aspnetcore # 14806](https://github.com/dotnet/aspnetcore/issues/14806).

## <a name="recommended-action"></a>Ação recomendada

Aplicativos que exigem certificados de cliente devem usar *netsh.exe* para definir a `clientcertnegotiation` opção como `enabled` . Para obter mais informações, consulte [netsh http Commands](/windows-server/networking/technologies/netsh/netsh-http).

Se você quiser que os certificados de cliente estejam habilitados somente para algumas partes do seu aplicativo, consulte as diretrizes em [certificados de cliente opcionais](/aspnet/core/security/authentication/certauth?view=aspnetcore-3.1#optional-client-certificates).

Se você precisar do comportamento antigo de renegociação, defina `HttpSysOptions.ClientCertificateMethod` como o valor antigo `ClientCertificateMethod.AllowRenegotiate` . Isso não é recomendado pelos motivos descritos acima e nas diretrizes vinculadas.

## <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.AspNetCore.Http.ConnectionInfo.ClientCertificate%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.ConnectionInfo.GetClientCertificateAsync%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.ClientCertificateMethod%2A?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

- `Overload:Microsoft.AspNetCore.Http.ConnectionInfo.ClientCertificate`
- `Overload:Microsoft.AspNetCore.Http.ConnectionInfo.GetClientCertificateAsync`
- `Overload:Microsoft.AspNetCore.Server.HttpSys.HttpSysOptions.ClientCertificateMethod`

-->
