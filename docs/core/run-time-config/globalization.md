---
title: Definições de configuração de globalização
description: Saiba mais sobre as configurações de tempo de execução que configuram aspectos de globalização de um aplicativo .NET Core, por exemplo, como ele analisa as datas japonesas.
ms.date: 05/18/2020
ms.topic: reference
ms.openlocfilehash: fc98e965093c28b75b9b66e4f1c9f147abd4680e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721901"
---
# <a name="run-time-configuration-options-for-globalization"></a>Opções de configuração de tempo de execução para globalização

## <a name="invariant-mode"></a>Modo invariável

- Determina se um aplicativo .NET Core é executado no modo inconstante de globalização sem acesso a dados e comportamento específicos de cultura.
- Se você omitir essa configuração, o aplicativo será executado com acesso aos dados culturais. Isso é equivalente a definir o valor como `false` .
- Para obter mais informações, consulte [modo invariável de globalização do .NET Core](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md).

| | Nome da configuração | Valores |
| - | - | - |
| **runtimeconfig.jsem** | `System.Globalization.Invariant` | `false` -acesso a dados culturais<br/>`true` -executar em modo invariável |
| **Propriedade do MSBuild** | `InvariantGlobalization` | `false` -acesso a dados culturais<br/>`true` -executar em modo invariável |
| **Variável de ambiente** | `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT` | `0` -acesso a dados culturais<br/>`1` -executar em modo invariável |

### <a name="examples"></a>Exemplos

*runtimeconfig.jsno* arquivo:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.Globalization.Invariant": true
      }
   }
}
```

Arquivo de projeto:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <InvariantGlobalization>true</InvariantGlobalization>
  </PropertyGroup>

</Project>
```

## <a name="era-year-ranges"></a>Intervalos de ano da era

- Determina se o intervalo verifica se os calendários que dão suporte a vários apagamentos são relaxados ou se as datas que excedem o intervalo de datas de uma época lançam um <xref:System.ArgumentOutOfRangeException> .
- Se você omitir essa configuração, as verificações de intervalo serão relaxadas. Isso é equivalente a definir o valor como `false` .
- Para obter mais informações, consulte [calendários, apagar e intervalos de datas: verificações de intervalo relaxadas](../../standard/datetime/working-with-calendars.md#calendars-eras-and-date-ranges-relaxed-range-checks).

| | Nome da configuração | Valores |
| - | - | - |
| **runtimeconfig.jsem** | `Switch.System.Globalization.EnforceJapaneseEraYearRanges` | `false` -verificações de intervalo relaxadas<br/>`true` -estouros causam uma exceção |
| **Variável de ambiente** | N/D | N/D |

## <a name="japanese-date-parsing"></a>Análise de data japonesa

- Determina se uma cadeia de caracteres que contém "1" ou "gannen" como o ano é analisada com êxito ou se apenas "1" tem suporte.
- Se você omitir essa configuração, as cadeias de caracteres que contêm "1" ou "gannen" como o ano é analisado com êxito. Isso é equivalente a definir o valor como `false` .
- Para obter mais informações, consulte [representar datas em calendários com vários apagar](../../standard/datetime/working-with-calendars.md#represent-dates-in-calendars-with-multiple-eras).

| | Nome da configuração | Valores |
| - | - | - |
| **runtimeconfig.jsem** | `Switch.System.Globalization.EnforceLegacyJapaneseDateParsing` | `false` -"Gannen" ou "1" tem suporte<br/>`true` -somente "1" é suportado |
| **Variável de ambiente** | N/D | N/D |

## <a name="japanese-year-format"></a>Formato de ano japonês

- Determina se o primeiro ano de uma era do calendário japonês é formatado como "gannen" ou como um número.
- Se você omitir essa configuração, o primeiro ano será formatado como "gannen". Isso é equivalente a definir o valor como `false` .
- Para obter mais informações, consulte [representar datas em calendários com vários apagar](../../standard/datetime/working-with-calendars.md#represent-dates-in-calendars-with-multiple-eras).

| | Nome da configuração | Valores |
| - | - | - |
| **runtimeconfig.jsem** | `Switch.System.Globalization.FormatJapaneseFirstYearAsANumber` | `false` -Formatar como "gannen"<br/>`true` -Formatar como número |
| **Variável de ambiente** | N/D | N/D |

## <a name="nls"></a>CRIOU

- Determina se o .NET usa o NLS (suporte a idioma nacional) ou as APIs de globalização do ICU (componentes internacionais para Unicode) para aplicativos do Windows. O .NET 5,0 e versões posteriores usam APIs de globalização ICU por padrão no Windows 10 pode ser 2019 atualização e versões posteriores.
- Se você omitir essa configuração, o .NET usará APIs de globalização ICU por padrão. Isso é equivalente a definir o valor como `false` .
- Para obter mais informações, consulte [APIs de globalização usam bibliotecas ICU no Windows](../compatibility/globalization/5.0/icu-globalization-api.md).

| | Nome da configuração | Valores | Introduzida |
| - | - | - | - |
| **runtimeconfig.jsem** | `System.Globalization.UseNls` | `false` -Usar APIs de globalização ICU<br/>`true` -Usar APIs de globalização NLS | .NET 5,0 |
| **Variável de ambiente** | `DOTNET_SYSTEM_GLOBALIZATION_USENLS` | `false` -Usar APIs de globalização ICU<br/>`true` -Usar APIs de globalização NLS | .NET 5,0 |
