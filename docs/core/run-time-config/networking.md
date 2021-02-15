---
title: Definições de configuração de rede
description: Saiba mais sobre as configurações de tempo de execução que configuram a rede para aplicativos .NET Core.
ms.date: 11/27/2019
ms.topic: reference
ms.openlocfilehash: bda608e83bb1b093d7d9b860de9607f6734720aa
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188296"
---
# <a name="run-time-configuration-options-for-networking"></a>Opções de configuração de tempo de execução para rede

## <a name="http2-protocol"></a>Protocolo HTTP/2

- Configura se o suporte para o protocolo HTTP/2 está habilitado.

- Introduzido no .NET Core 3,0.

- Somente .NET Core 3,0: se você omitir essa configuração, o suporte para o protocolo HTTP/2 será desabilitado. Isso é equivalente a definir o valor como `false` .

- .NET Core 3,1 e .NET 5 +: se você omitir essa configuração, o suporte para o protocolo HTTP/2 será habilitado. Isso é equivalente a definir o valor como `true` .

| | Nome da configuração | Valores |
| - | - | - |
| **runtimeconfig.jsem** | `System.Net.Http.SocketsHttpHandler.Http2Support` | `false` -desabilitado<br/>`true` -habilitado |
| **Variável de ambiente** | `DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_HTTP2SUPPORT` | `0` -desabilitado<br/>`1` -habilitado |

## <a name="usesocketshttphandler"></a>UseSocketsHttpHandler

- Configura se <xref:System.Net.Http.HttpClientHandler?displayProperty=nameWithType> <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> o usa ou pilhas de protocolo http mais antigas ( <xref:System.Net.Http.WinHttpHandler> no Windows e `CurlHandler` uma classe interna implementada sobre [libcurl](https://curl.haxx.se/libcurl/), no Linux).

  > [!NOTE]
  > Você pode estar usando APIs de rede de alto nível em vez de instanciar diretamente a <xref:System.Net.Http.HttpClientHandler> classe. Essa configuração também afeta qual pilha de protocolo HTTP é usada por APIs de rede de alto nível, incluindo <xref:System.Net.Http.HttpClient> e [HttpClientFactory](/previous-versions/aspnet/hh995280(v=vs.118)).

- Se você omitir essa configuração, o <xref:System.Net.Http.HttpClientHandler> usará <xref:System.Net.Http.SocketsHttpHandler> . Isso é equivalente a definir o valor como `true` .

- Você pode definir essa configuração programaticamente chamando o <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> método.

| | Nome da configuração | Valores |
| - | - | - |
| **runtimeconfig.jsem** | `System.Net.Http.UseSocketsHttpHandler` | `true` – habilita o uso de <xref:System.Net.Http.SocketsHttpHandler><br/>`false` – habilita o uso do <xref:System.Net.Http.WinHttpHandler> no Windows ou [libcurl](https://curl.haxx.se/libcurl/) no Linux |
| **Variável de ambiente** | `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER` | `1` – habilita o uso de <xref:System.Net.Http.SocketsHttpHandler><br/>`0` – habilita o uso do <xref:System.Net.Http.WinHttpHandler> no Windows ou [libcurl](https://curl.haxx.se/libcurl/) no Linux |

> [!NOTE]
> A partir do .NET 5, a `System.Net.Http.UseSocketsHttpHandler` configuração não está mais disponível.

## <a name="latin1-headers-net-core-31-only"></a>Cabeçalhos latino1 (somente .NET Core 3,1)

- Essa opção permite relaxar a validação do cabeçalho HTTP, permitindo <xref:System.Net.Http.SocketsHttpHandler> enviar caracteres codificados para ISO-8859-1 (latino-1) nos cabeçalhos.

- Se você omitir essa configuração, uma tentativa de enviar um caractere não-ASCII resultará em <xref:System.Net.Http.HttpRequestException> . Isso é equivalente a definir o valor como `false` .

| | Nome da configuração | Valores |
| - | - | - |
| **runtimeconfig.jsem** | `System.Net.Http.SocketsHttpHandler.AllowLatin1Headers` | `false` -desabilitado<br/>`true` -habilitado |
| **Variável de ambiente** | `DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_ALLOWLATIN1HEADERS` | `0` -desabilitado<br/>`1` -habilitado |

> [!NOTE]
> Essa opção só está disponível no .NET Core 3,1 desde a versão 3.1.9, e não nas versões anteriores ou posteriores. No .NET 5, recomendamos o uso do <xref:System.Net.Http.SocketsHttpHandler.RequestHeaderEncodingSelector> .
