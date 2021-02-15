---
ms.openlocfilehash: 958dede03e1c15f69f4ee676f13713ff43c29e96
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032290"
---
### <a name="logging-debuglogger-class-made-internal"></a>Log: classe DebugLogger criada internamente

Antes do ASP.NET Core 3,0, o `DebugLogger` modificador de acesso foi `public` . No ASP.NET Core 3,0, o modificador de acesso foi alterado para `internal` .

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="reason-for-change"></a>Motivo da alteração

A alteração está sendo feita para:

* Impor consistência com outras implementações de agente, como `ConsoleLogger` .
* Reduza a superfície da API.

#### <a name="recommended-action"></a>Ação recomendada

Use o <xref:Microsoft.Extensions.Logging.DebugLoggerFactoryExtensions.AddDebug%2A> `ILoggingBuilder` método de extensão para habilitar o log de depuração. <xref:Microsoft.Extensions.Logging.Debug.DebugLoggerProvider> também é ainda `public` no caso de o serviço precisar ser registrado manualmente.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.Extensions.Logging.Debug.DebugLogger?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.Extensions.Logging.Debug.DebugLogger`

-->
