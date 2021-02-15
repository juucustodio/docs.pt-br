---
title: 'Alteração significativa: Kestrel: HTTP/2 desabilitado via TLS em versões incompatíveis do Windows'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado Kestrel: HTTP/2 desabilitado em TLS em versões incompatíveis do Windows'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: befd393795f3e1859d391bca513dd9856101d295
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760482"
---
# <a name="kestrel-http2-disabled-over-tls-on-incompatible-windows-versions"></a>Kestrel: HTTP/2 desabilitado via TLS em versões incompatíveis do Windows

Para habilitar o HTTP/2 pela TLS (segurança da camada de transporte) no Windows, dois requisitos precisam ser atendidos:

- Suporte à ALPN (negociação de protocolo Application-Layer), que está disponível a partir do Windows 8.1 e do Windows Server 2012 R2.
- Um conjunto de codificações compatível com HTTP/2, que está disponível a partir do Windows 10 e do Windows Server 2016.

Dessa forma, o comportamento do Kestrel quando HTTP/2 sobre TLS é configurado foi alterado para:

- `Http1`Faça o downgrade para e registre uma mensagem no `Information` nível quando [ListenerOptions. HttpProtocols](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.httpprotocols) for definido como `Http1AndHttp2` . `Http1AndHttp2` é o valor padrão do `ListenOptions.HttpProtocols`.
- Lança um `NotSupportedException` quando `ListenOptions.HttpProtocols` é definido como `Http2` .

Para obter uma discussão, veja Issue [dotnet/aspnetcore # 23068](https://github.com/dotnet/aspnetcore/issues/23068).

## <a name="version-introduced"></a>Versão introduzida

ASP.NET Core 5,0 Preview 7

## <a name="old-behavior"></a>Comportamento antigo

A tabela a seguir descreve o comportamento quando HTTP/2 em TLS é configurado.

| Protocolos | Windows 7,<br />Windows Server 2008 R2,<br />ou anterior | Windows 8,<br />Windows Server 2012 | Windows 8.1<br />Windows Server 2012 R2 | Windows 10,<br />Windows Server 2016,<br /> ou mais recente |
|---------------|-----------------------------------------------|--------------------------------|-------------------------------------|------------------------------------------|
| `Http2`         | Throw `NotSupportedException`                   | Erro durante o handshake de TLS     | Erro durante o handshake de TLS &ast;     | Nenhum erro |
| `Http1AndHttp2` | Fazer downgrade para `Http1`                    | Fazer downgrade para `Http1`     | Erro durante o handshake de TLS &ast;     | Nenhum erro |

&ast; Configure conjuntos de codificação compatíveis para habilitar esses cenários.

## <a name="new-behavior"></a>Novo comportamento

A tabela a seguir descreve o comportamento quando HTTP/2 em TLS é configurado.

| Protocolos | Windows 7,<br />Windows Server 2008 R2,<br />ou anterior | Windows 8,<br />Windows Server 2012 | Windows 8.1<br />Windows Server 2012 R2 | Windows 10,<br />Windows Server 2016,<br /> ou mais recente |
|---------------|-----------------------------------------------|--------------------------------|-------------------------------------|------------------------------------------|
| `Http2`         | Throw `NotSupportedException`                   | Throw `NotSupportedException`     | Lançar `NotSupportedException`&ast;&ast;     | Nenhum erro |
| `Http1AndHttp2` | Fazer downgrade para `Http1`                    | Fazer downgrade para `Http1`     | Fazer downgrade para `Http1`&ast;&ast;     | Nenhum erro |

&ast;&ast; Configure conjuntos de codificação compatíveis e defina a opção de contexto do aplicativo `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2` como `true` para habilitar esses cenários.

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração garante que os erros de compatibilidade para HTTP/2 sobre TLS em versões mais antigas do Windows sejam exibidos como antes e o mais claramente possível.

## <a name="recommended-action"></a>Ação recomendada

Verifique se o HTTP/2 sobre TLS está desabilitado em versões incompatíveis do Windows. O Windows 8.1 e o Windows Server 2012 R2 são incompatíveis, pois não têm as codificações necessárias por padrão. No entanto, é possível atualizar as definições de configuração do computador para usar codificações compatíveis com HTTP/2. Para obter mais informações, consulte [conjuntos de criptografia TLS em Windows 8.1](/windows/win32/secauthn/tls-cipher-suites-in-windows-8-1). Uma vez configurado, o HTTP/2 sobre TLS em Kestrel deve ser habilitado definindo a opção de contexto do aplicativo `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2` . Por exemplo:

```csharp
AppContext.SetSwitch("Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2", true);
```

Nenhum suporte subjacente foi alterado. Por exemplo, HTTP/2 sobre TLS nunca funcionou no Windows 8 ou no Windows Server 2012. Essa alteração modifica como os erros nesses cenários sem suporte são apresentados.

## <a name="affected-apis"></a>APIs afetadas

Nenhum

<!--

### Category

ASP.NET Core

### Affected APIs

Not detectable via API analysis

-->
