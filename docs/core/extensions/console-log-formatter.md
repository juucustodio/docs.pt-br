---
title: Formatação de log de console
description: Saiba como usar a formatação de log de console disponível ou implementar a formatação de log personalizada para seus aplicativos .NET.
author: IEvangelist
ms.author: dapine
ms.date: 12/17/2020
ms.openlocfilehash: 0ec8fc2018febe4273aa646d1682be197933f925
ms.sourcegitcommit: 3d6d6595a03915f617349781f455f838a44b0f44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97700815"
---
# <a name="console-log-formatting"></a>Formatação de log de console

No .NET 5, o suporte à formatação personalizada foi adicionado aos logs do console no `Microsoft.Extensions.Logging.Console` namespace. Há três opções de formatação predefinidas disponíveis: [`Simple`](#simple) , [`Systemd`](#systemd) e [`Json`](#json) .

> [!IMPORTANT]
> Anteriormente, a <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerFormat> Enumeração permitia selecionar o formato de log desejado, legível por humanos, que era o `Default` , ou linha única, também conhecido como `Systemd` . No entanto, elas **não** eram personalizáveis e agora estão preteridas.

Neste artigo, você aprenderá sobre os formatadores de log do console. O código-fonte de exemplo demonstra como:

- Registrar um novo formatador
- Selecione um formatador registrado para usar
  - Por meio de código ou [configuração](configuration.md)
- Implementar um formatador personalizado
  - Atualizar configuração via <xref:Microsoft.Extensions.Options.IOptionsMonitor%601>
  - Habilitar formatação de cor personalizada

## <a name="register-formatter"></a>Registrar formatador

O [ `Console` provedor de log](logging-providers.md#console) tem vários formatadores predefinidos e expõe a capacidade de criar seu próprio formatador personalizado. Para registrar qualquer um dos formatadores disponíveis, use o `Add{Type}Console` método de extensão correspondente:

| Tipos disponíveis | Método para registrar tipo |
|--|--|
| <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Json?displayProperty=nameWithType> | <xref:Microsoft.Extensions.Logging.ConsoleLoggerExtensions.AddJsonConsole%2A?displayProperty=nameWithType> |
| <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Simple?displayProperty=nameWithType> | <xref:Microsoft.Extensions.Logging.ConsoleLoggerExtensions.AddSimpleConsole%2A?displayProperty=nameWithType> |
| <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Systemd?displayProperty=nameWithType> | <xref:Microsoft.Extensions.Logging.ConsoleLoggerExtensions.AddSystemdConsole%2A?displayProperty=nameWithType> |

### <a name="simple"></a>Simples

Para usar o `Simple` formatador do console, registre-o com `AddSimpleConsole` :

:::code language="csharp" source="snippets/logging/console-formatter-simple/Program.cs" highlight="11-16":::

No código-fonte de exemplo anterior, o <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Simple?displayProperty=nameWithType> formatador foi registrado. Ele fornece aos logs a capacidade de não apenas encapsular informações como tempo e nível de log em cada mensagem de log, mas também permite a inserção de cor ANSI e o recuo de mensagens.

### <a name="systemd"></a>Systemd

O <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Systemd?displayProperty=nameWithType> agente do console do:

- Usa o formato e as severidades do nível de log "syslog"
- Não **formata mensagens** com cores
- Sempre registra mensagens em uma única linha

Isso é normalmente útil para contêineres, que geralmente fazem uso de `Systemd` log de console. Com o .NET 5, o `Simple` agente de log do console também permite uma versão compactada que registra em uma única linha, além de permitir a desabilitação de cores, conforme mostrado em um exemplo anterior.

:::code language="csharp" source="snippets/logging/console-formatter-systemd/Program.cs" highlight="11-15":::

### <a name="json"></a>Json

Para gravar logs em um formato JSON, o `Json` formatador do console é usado. O código-fonte de exemplo mostra como um aplicativo ASP.NET Core pode registrá-lo. Usando o `webapp` modelo, crie um novo aplicativo ASP.NET Core com o [novo comando dotnet](../tools/dotnet-new.md) :

```dotnetcli
dotnet new webapp -o Console.ExampleFormatters.Json
```

Ao executar o aplicativo, usando o código de modelo, você obtém o formato de log padrão abaixo:

```
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: https://localhost:5001
```

Por padrão, o `Simple` formatador de log do console é selecionado com a configuração padrão. Você altera isso chamando `AddJsonConsole` no *Program.cs*:

:::code language="csharp" source="snippets/logging/console-formatter-json/Program.cs" highlight="17-26":::

Execute o aplicativo novamente, com a alteração acima, a mensagem de log agora está formatada como JSON:

:::code language="json" source="snippets/logging/console-formatter-json/example-output.json":::

> [!TIP]
> O `Json` formatador do console, por padrão, registra cada mensagem em uma única linha. Para torná-lo mais legível ao configurar o formatador, defina <xref:System.Text.Json.JsonWriterOptions.Indented?displayProperty=nameWithType> como `true` .

## <a name="set-formatter-with-configuration"></a>Definir formatador com configuração

Os exemplos anteriores mostraram como registrar um formatador programaticamente. Como alternativa, isso pode ser feito com a [configuração](configuration.md). Considere o código-fonte do aplicativo Web anterior, se você atualizar o *appsettings.jsno* arquivo em vez de chamar `ConfigureLogging` no arquivo *Program.cs* , poderá obter o mesmo resultado. O `appsettings.json` arquivo atualizado configuraria o formatador da seguinte maneira:

:::code language="json" source="snippets/logging/console-formatter-json/appsettings.json" highlight="14-23":::

Os dois valores de chave que precisam ser definidos são `"FormatterName"` e `"FormatterOptions"` . Se um formatador com o valor definido para `"FormatterName"` já estiver registrado, esse formatador será selecionado e suas propriedades poderão ser configuradas desde que sejam fornecidas como uma chave dentro do `"FormatterOptions"` nó. Os nomes de formatadores predefinidos são reservados em <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames> :

- <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Json?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Simple?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterNames.Systemd?displayProperty=nameWithType>

## <a name="implement-a-custom-formatter"></a>Implementar um formatador personalizado

Para implementar um formatador personalizado, você precisa:

- Criar uma subclasse de <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatter> , representa seu formatador personalizado
- Registrar seu formatador personalizado com
  - <xref:Microsoft.Extensions.Logging.ConsoleLoggerExtensions.AddConsole%2A?displayProperty=nameWithType>
  - <xref:Microsoft.Extensions.Logging.ConsoleLoggerExtensions.AddConsoleFormatter%60%602(Microsoft.Extensions.Logging.ILoggingBuilder,System.Action{%60%601})?displayProperty=nameWithType>

Crie um método de extensão para lidar com isso para você:

:::code language="csharp" source="snippets/logging/console-formatter-custom/ConsoleLoggerExtensions.cs" highlight="11-12":::

Os `CustomOptions` são definidos da seguinte maneira:

:::code language="csharp" source="snippets/logging/console-formatter-custom/CustomOptions.cs":::

No código anterior, as opções são uma subclasse de <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterOptions> .

A `AddConsoleFormatter` API:

- Registra uma subclasse de `ConsoleFormatter`
- Configuração de identificadores:
  - Usa um token de alteração para sincronizar atualizações, com base no [padrão de opções](options.md)e na interface [IOptionsMonitor](xref:Microsoft.Extensions.Options.IOptionsMonitor%601)

:::code language="csharp" source="snippets/logging/console-formatter-custom/Program.cs" highlight="11-12":::

Defina uma `CustomerFormatter` subclasse de `ConsoleFormatter` :

:::code language="csharp" source="snippets/logging/console-formatter-custom/CustomFormatter.cs" highlight="24-45":::

A `CustomFormatter.Write<TState>` API anterior determina qual texto é encapsulado em torno de cada mensagem de log. Um padrão `ConsoleFormatter` deve ser capaz de encapsular escopos, carimbos de data/hora e nível de severidade de logs no mínimo. Além disso, você pode codificar as cores ANSI nas mensagens de log e também fornecer recuos desejados. A implementação do não `CustomFormatter.Write<TState>` tem esses recursos.

Para inspiração ao personalizar ainda mais a formatação, consulte as implementações existentes no `Microsoft.Extensions.Logging.Console` namespace:

- [SimpleConsoleFormatter](https://github.com/dotnet/runtime/blob/master/src/libraries/Microsoft.Extensions.Logging.Console/src/SimpleConsoleFormatter.cs).
- [SystemdConsoleFormatter](https://github.com/dotnet/runtime/blob/master/src/libraries/Microsoft.Extensions.Logging.Console/src/SystemdConsoleFormatter.cs)
- [JsonConsoleFormatter](https://github.com/dotnet/runtime/blob/master/src/libraries/Microsoft.Extensions.Logging.Console/src/JsonConsoleFormatter.cs)

## <a name="implement-custom-color-formatting"></a>Implementar a formatação de cor personalizada

Para habilitar corretamente os recursos de cores em seu formatador de log personalizado, você pode estender o, <xref:Microsoft.Extensions.Logging.Console.SimpleConsoleFormatterOptions> pois ele tem uma <xref:Microsoft.Extensions.Logging.Console.SimpleConsoleFormatterOptions.ColorBehavior?displayProperty=nameWithType> propriedade que pode ser útil para habilitar cores em logs.

Crie um `CustomColorOptions` que derive de `SimpleConsoleFormatterOptions` :

:::code language="csharp" source="snippets/logging/console-formatter-custom/CustomColorOptions.cs" highlight="5":::

Em seguida, escreva alguns métodos de extensão em uma `TextWriterExtensions` classe que permitem incorporar convenientemente as cores codificadas ANSI em mensagens de log formatadas:

:::code language="csharp" source="snippets/logging/console-formatter-custom/TextWriterExtensions.cs":::

Um formatador de cor personalizado que manipula a aplicação de cores personalizadas pode ser definido da seguinte maneira:

:::code language="csharp" source="snippets/logging/console-formatter-custom/CustomColorFormatter.cs" highlight="15-18,52-65":::

Quando você executar o aplicativo, os logs mostrarão a `CustomPrefix` mensagem na cor verde quando `FormatterOptions.ColorBehavior` for `Enabled` .

> [!NOTE]
> Quando <xref:Microsoft.Extensions.Logging.Console.LoggerColorBehavior> é `Disabled` , as mensagens de log _não_ interpretam códigos de cores ANSI inseridos nas mensagens de log. Em vez disso, eles geram a mensagem bruta. Considere o seguinte exemplo:
>
> ```csharp
> logger.LogInformation("Random log \x1B[42mwith green background\x1B[49m message");
> ```
>
> Isso produziria a cadeia de caracteres textual e _não_ é colorido.
>
> ```output
> Random log \x1B[42mwith green background\x1B[49m message
> ```

## <a name="see-also"></a>Veja também

- [Registro em log no .NET](logging.md)
- [Implementar um provedor de log personalizado no .NET](custom-logging-provider.md)
- [Registro em log de alto desempenho no .NET](high-performance-logging.md)
