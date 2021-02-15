---
title: 'Alteração significativa: HTTP: instâncias de HttpClient criadas por códigos de status de inteiro de log IHttpClientFactory'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado HTTP: instâncias de HttpClient criadas por códigos de status de inteiro de log IHttpClientFactory'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 964c0a65a07816acea8016d42a66a6bf84aba7c4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760314"
---
# <a name="http-httpclient-instances-created-by-ihttpclientfactory-log-integer-status-codes"></a>HTTP: instâncias de HttpClient criadas por códigos de status de inteiro de log IHttpClientFactory

<xref:System.Net.Http.HttpClient> instâncias criadas por <xref:System.Net.Http.IHttpClientFactory> códigos de status HTTP de log como inteiros em vez de com nomes de código de status.

## <a name="version-introduced"></a>Versão introduzida

5,0 visualização 1

## <a name="old-behavior"></a>Comportamento antigo

O registro em log usa as descrições textuais dos códigos de status HTTP. Considere as seguintes mensagens de log:

```output
Received HTTP response after 56.0044ms - OK
End processing HTTP request after 70.0862ms - OK
```

## <a name="new-behavior"></a>Novo comportamento

O registro em log usa os valores inteiros dos códigos de status HTTP. Considere as seguintes mensagens de log:

```output
Received HTTP response after 56.0044ms - 200
End processing HTTP request after 70.0862ms - 200
```

## <a name="reason-for-change"></a>Motivo da alteração

O comportamento original desse log é inconsistente com outras partes do ASP.NET Core que sempre usaram valores inteiros. A inconsistência torna os logs difíceis de consultar por meio de sistemas de registro estruturado, como [Elasticsearch](https://www.elastic.co/elasticsearch/). Para obter mais contexto, consulte [dotnet/Extensions # 1549](https://github.com/dotnet/extensions/issues/1549).

O uso de valores inteiros é mais flexível que o texto, pois permite consultas em intervalos de valores.

A adição de outro valor de log para capturar o código de status inteiro foi considerada. Infelizmente, isso introduziria outra inconsistência com o restante do ASP.NET Core. O log de HttpClient e o servidor HTTP/log de hospedagem usam o mesmo `StatusCode` nome de chave já.

## <a name="recommended-action"></a>Ação recomendada

A melhor opção é atualizar as consultas de log para usar os valores inteiros de códigos de status. Essa opção pode causar alguma dificuldade para gravar consultas em várias versões de ASP.NET Core. No entanto, o uso de inteiros para essa finalidade é muito mais flexível para consultar logs.

Se você precisar forçar a compatibilidade com o comportamento antigo e usar códigos de status textuais, substitua o `IHttpClientFactory` log pelo seu próprio:

1. Copie as versões 3,1 do .NET Core das seguintes classes em seu projeto:

    * [LoggingHttpMessageHandlerBuilderFilter](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingHttpMessageHandlerBuilderFilter.cs)
    * [LoggingHttpMessageHandler](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingHttpMessageHandler.cs)
    * [LoggingScopeHttpMessageHandler](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingScopeHttpMessageHandler.cs)
    * [HttpHeadersLogValue](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/HttpHeadersLogValue.cs)

1. Renomeie as classes para evitar conflitos com tipos públicos no pacote NuGet [Microsoft. Extensions. http](https://www.nuget.org/packages/Microsoft.Extensions.Http) .

1. Substitua a implementação interna de `LoggingHttpMessageHandlerBuilderFilter` pela sua própria no método do projeto `Startup.ConfigureServices` . Por exemplo:

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        // Other service registrations go first. Code omitted for brevity.

        // Place the following after all AddHttpClient registrations.
        services.RemoveAll<IHttpMessageHandlerBuilderFilter>();

        services.AddSingleton<IHttpMessageHandlerBuilderFilter,
                              MyLoggingHttpMessageHandlerBuilderFilter>();
    }
    ```

## <a name="affected-apis"></a>APIs afetadas

<xref:System.Net.Http.HttpClient?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`T:System.Net.Http.HttpClient`

-->
