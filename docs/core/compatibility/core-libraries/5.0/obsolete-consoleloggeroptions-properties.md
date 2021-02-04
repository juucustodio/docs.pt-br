---
title: 'Alteração significativa: Propriedades obsoletas em ConsoleLoggerOptions'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que o tipo ConsoleLoggerFormat e algumas propriedades em ConsoleLoggerOptions agora são obsoletos.
ms.date: 11/01/2020
ms.openlocfilehash: bd039dfa84ae3399d7fb36f992010a9a3c9f6ddf
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99548377"
---
# <a name="obsolete-properties-on-consoleloggeroptions"></a>Propriedades obsoletas em ConsoleLoggerOptions

O <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerFormat?displayProperty=nameWithType> tipo e algumas propriedades em <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions> agora estão obsoletos.

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerFormat?displayProperty=nameWithType> tipo e várias propriedades <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions> são obsoletos. As propriedades obsoletas são:

- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format?displayProperty=nameWithType>

Com a introdução de novos formatadores, essas propriedades agora estão disponíveis nos formatadores individuais.

## <a name="reason-for-change"></a>Motivo da alteração

A <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format> propriedade é um tipo de enumeração, que não pode representar um formatador personalizado.

As propriedades restantes foram definidas <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions> e aplicadas a ambos os formatos internos para logs do console. No entanto, com a introdução de uma nova API de formatador, faz mais sentido para que a formatação seja representada nas opções específicas do formatador. Essa alteração fornece melhor separação entre os formatadores do agente e do agente de log.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- Use a nova <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.FormatterName?displayProperty=nameWithType> propriedade no lugar da <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format?displayProperty=nameWithType> propriedade. Por exemplo:

  ```csharp
  loggingBuilder.AddConsole(options =>
  {
    options.FormatterName = ConsoleFormatterNames.Systemd;
  });
  ```

  Há várias diferenças entre <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.FormatterName> e <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format> :

  - <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format> tem apenas duas opções possíveis: `Default` e `Systemd` .
  - <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.FormatterName> não diferencia maiúsculas de minúsculas e pode ser qualquer cadeia de caracteres. Os nomes internos reservados são `Simple` , `Systemd` e `Json` (.NET 5,0 e posterior).
  - `"Format": "Systemd"` mapeia para `"FormatterName": "Systemd"` .
  - `"Format": "Default"` mapeia para `"FormatterName": "Simple"` .

- Para as <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors> <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes> Propriedades,, e <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat> <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp> , use a propriedade correspondente nos <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterOptions> tipos novo, <xref:Microsoft.Extensions.Logging.Console.JsonConsoleFormatterOptions> ou <xref:Microsoft.Extensions.Logging.Console.SimpleConsoleFormatterOptions> . Por exemplo, a configuração correspondente para <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors?displayProperty=nameWithType> é <xref:Microsoft.Extensions.Logging.Console.SimpleConsoleFormatterOptions.ColorBehavior?displayProperty=nameWithType> .

  Código anterior:

  ```csharp
  loggingBuilder.AddConsole(options =>
  {
      options.DisableColors = true;
  });
  ```

  Novo código:

  ```csharp
  loggingBuilder.AddSimpleConsole(options =>
  {
      options.ColorBehavior = LoggerColorBehavior.Disabled;
  });
  ```

Os dois trechos de código JSON a seguir mostram como o arquivo de configuração é alterado. Arquivo de configuração antigo:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "None",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    },

    "Console": {
      "LogLevel": {
        "Default": "Information"
      },
      "Format": "Systemd",
      "IncludeScopes": true,
      "TimestampFormat": "HH:mm:ss",
      "UseUtcTimestamp": true
    }
  },
  "AllowedHosts": "*"
}
```

Novo arquivo de configuração:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "None",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    },

    "Console": {
      "LogLevel": {
        "Default": "Information"
      },
      "FormatterName": "Systemd",
      "FormatterOptions": {
        "IncludeScopes": true,
        "TimestampFormat": "HH:mm:ss",
        "UseUtcTimestamp": true
      }
    }
  },
  "AllowedHosts": "*"
}
```

## <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format?displayProperty=fullName>

<!--

#### Category

- Core .NET libraries
- ASP.NET

### Affected APIs

- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format`

-->
