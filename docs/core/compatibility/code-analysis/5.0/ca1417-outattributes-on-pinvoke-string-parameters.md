---
title: 'Alteração significativa: CA1417: OutAttribute no parâmetro de cadeia de caracteres para P/Invoke'
description: Saiba mais sobre a alteração significativa no .NET 5,0 causada pela habilitação da regra de análise de código CA1417.
ms.date: 09/29/2020
ms.openlocfilehash: 3316d07108ec7f9da985494413336cba6d560dc9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760306"
---
# <a name="warning-ca1417-outattribute-on-string-parameter-for-pinvoke"></a>Aviso CA1417: OutAttribute no parâmetro de cadeia de caracteres para P/Invoke

A regra do analisador de código .NET [CA1417](/visualstudio/code-quality/ca1417) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para qualquer definição de método de [invocação de plataforma (P/Invoke)](../../../../standard/native-interop/pinvoke.md) , em que um <xref:System.String> parâmetro é passado por valor e marcado com <xref:System.Runtime.InteropServices.OutAttribute> .

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../fundamentals/code-analysis/overview.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA1417](/visualstudio/code-quality/ca1417). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

Regra CA1417 flags [P/Invoke](../../../../standard/native-interop/pinvoke.md) definições de método em que um <xref:System.String> parâmetro é marcado com o <xref:System.Runtime.InteropServices.OutAttribute> atributo e é passado por valor. Por exemplo:

```csharp
[DllImport("MyLibrary")]
private static extern void PIMethod([Out] string s);
```

O tempo de execução do .NET mantém uma tabela, chamada de pool do estagiário, que contém uma única referência a cada cadeia de caracteres literal exclusiva em um programa. Se uma cadeia de caracteres do InterNIC marcada com <xref:System.Runtime.InteropServices.OutAttribute> for passada por valor para um método P/Invoke, o tempo de execução poderá ser desestabilizado. Para obter mais informações sobre o InterNIC da cadeia de caracteres, consulte comentários para <xref:System.String.Intern(System.String)?displayProperty=nameWithType> .

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- Se você precisar realizar o marshaling dos dados de cadeia de caracteres modificados de volta para o chamador, passe a cadeia de caracteres por referência.

  ```csharp
  [DllImport("MyLibrary")]
  private static extern void PIMethod(out string s);
  ```

- Se você não precisar realizar o marshaling dos dados de cadeia de caracteres modificados de volta para o chamador, simplesmente remova o <xref:System.Runtime.InteropServices.OutAttribute> .

  ```csharp
  [DllImport("MyLibrary")]
  private static extern void PIMethod(string s);
  ```

  Para obter mais informações, consulte [CA1417](/visualstudio/code-quality/ca1417).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).

## <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

### Affected APIs

Not detectable via API analysis.

### Category

Code analysis

-->
