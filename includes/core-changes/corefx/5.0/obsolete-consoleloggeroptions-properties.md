---
ms.openlocfilehash: e92fe8364800b1775f0acc31d67aef66a42d0b95
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465866"
---
### <a name="obsolete-properties-on-consoleloggeroptions"></a>Propriedades obsoletas em ConsoleLoggerOptions

O <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerFormat?displayProperty=nameWithType> tipo e algumas propriedades em <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions> agora estão obsoletos.

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerFormat?displayProperty=nameWithType> tipo e várias propriedades <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions> são obsoletos. As propriedades obsoletas são:

- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format?displayProperty=nameWithType>

Com a introdução de novos formatadores, essas propriedades agora estão disponíveis nos formatadores individuais.

#### <a name="reason-for-change"></a>Motivo da alteração

A <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format> propriedade é um tipo de enumeração, que não pode representar um formatador personalizado.

As propriedades restantes foram definidas <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions> e aplicadas a ambos os formatos internos para logs do console. No entanto, com a introdução de uma nova API de formatador, faz mais sentido para que a formatação seja representada nas opções específicas do formatador. Essa alteração fornece melhor separação entre os formatadores do agente e do agente de log.

#### <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

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

- Para as <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors> <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes> Propriedades,, e <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat> <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp> , use a propriedade correspondente nos <xref:Microsoft.Extensions.Logging.Console.ConsoleFormatterOptions> tipos novo, <xref:Microsoft.Extensions.Logging.Console.JsonConsoleFormatterOptions> ou <xref:Microsoft.Extensions.Logging.Console.SimpleConsoleFormatterOptions> . Por exemplo:

  ```csharp
  loggingBuilder.AddSimpleConsole(options =>
  {
      options.DisableColors = true;
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

#### <a name="category"></a>Categoria

- Bibliotecas principais do .NET
- ASP.NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp?displayProperty=fullName>
- <xref:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format?displayProperty=fullName>

<!--

#### Affected APIs

- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.DisableColors`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.IncludeScopes`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.TimestampFormat`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.UseUtcTimestamp`
- `P:Microsoft.Extensions.Logging.Console.ConsoleLoggerOptions.Format`

-->
