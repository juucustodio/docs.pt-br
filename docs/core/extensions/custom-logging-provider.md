---
title: Implementar um provedor de log personalizado no .NET
description: Saiba como implementar um provedor de log personalizado em seus aplicativos .NET.
author: IEvangelist
ms.author: dapine
ms.date: 09/25/2020
ms.topic: how-to
ms.openlocfilehash: 3a0af6296c2ade15ff1b75dce5a5f99bfe235ebf
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91614670"
---
# <a name="implement-a-custom-logging-provider-in-net"></a>Implementar um provedor de log personalizado no .NET

Há muitos [provedores de log](logging-providers.md) disponíveis para necessidades de log comuns. Talvez seja necessário implementar um personalizado <xref:Microsoft.Extensions.Logging.ILoggerProvider> quando um dos provedores disponíveis não atender às suas necessidades de aplicativo. Neste artigo, você aprenderá a implementar um provedor de log personalizado que pode ser usado para colorir logs no console do.

### <a name="sample-custom-logger-configuration"></a>Configuração de agente de log personalizado de exemplo

O exemplo cria entradas de console de cores diferentes por nível de log e ID de evento usando o seguinte tipo de configuração:

:::code language="csharp" source="snippets/configuration/console-custom-logging/ColorConsoleLoggerConfiguration.cs":::

O código anterior define o nível padrão como `Information` , a cor para `Green` e o `EventId` é implicitamente `0` .

### <a name="create-the-custom-logger"></a>Criar o agente de log personalizado

O `ILogger` nome da categoria de implementação normalmente é a origem do log. Por exemplo, o tipo em que o agente é criado:

:::code language="csharp" source="snippets/configuration/console-custom-logging/ColorConsoleLogger.cs":::

O código anterior:

- Cria uma instância de agente por nome de categoria.
- Faz `logLevel == _config.LogLevel` o check-in `IsEnabled` , de modo que cada `logLevel` um tem um agente exclusivo. Os agentes também devem ser habilitados para todos os níveis de log mais altos:

:::code language="csharp" source="snippets/configuration/console-custom-logging/ColorConsoleLogger.cs" range="16-17":::

## <a name="custom-logger-provider"></a>Provedor de agente personalizado

O `ILoggerProvider` objeto é responsável pela criação de instâncias de agente. Talvez não seja necessário criar uma instância de agente por categoria, mas isso faz sentido para alguns agentes, como NLog ou log4net. Fazendo isso, você também pode escolher destinos de saída de log diferentes por categoria, se necessário:

:::code language="csharp" source="snippets/configuration/console-custom-logging/ColorConsoleLoggerProvider.cs":::

No código anterior, <xref:Microsoft.Build.Logging.LoggerDescription.CreateLogger%2A> cria uma única instância do `ColorConsoleLogger` nome por categoria e a armazena no [`ConcurrentDictionary<TKey,TValue>`](/dotnet/api/system.collections.concurrent.concurrentdictionary-2) .

## <a name="usage-and-registration-of-the-custom-logger"></a>Uso e registro do agente de log personalizado

Para adicionar o provedor de log personalizado e o agente correspondente, adicione um <xref:Microsoft.Extensions.Logging.ILoggerProvider> com <xref:Microsoft.Extensions.Logging.ILoggingBuilder> do <xref:Microsoft.Extensions.Hosting.HostingHostBuilderExtensions.ConfigureLogging(Microsoft.Extensions.Hosting.IHostBuilder,System.Action{Microsoft.Extensions.Logging.ILoggingBuilder})?displayProperty=nameWithType> :

:::code language="csharp" source="snippets/configuration/console-custom-logging/Program.cs" range="23-39":::

O `ILoggingBuilder` cria uma ou mais `ILogger` instâncias. As `ILogger` instâncias são usadas pelo Framework para registrar as informações.

Para o código anterior, forneça pelo menos um método de extensão para `ILoggerFactory` :

:::code language="csharp" source="snippets/configuration/console-custom-logging/Extensions/ColorConsoleLoggerExtensions.cs":::

A execução desse aplicativo simples será processada da seguinte janela do console:

:::image type="content" source="media/color-console-logger.png" alt-text="Saída de exemplo de agente do console de cores":::

## <a name="see-also"></a>Confira também

- [Registro em log no .net](logging.md).
- [Provedores de log no .net](logging-providers.md).
- [Registro em log de alto desempenho no .net](high-performance-logging.md).
