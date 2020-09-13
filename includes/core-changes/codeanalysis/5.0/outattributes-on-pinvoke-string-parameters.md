---
ms.openlocfilehash: ada458ffeeba95d4989507f90c789b159f359797
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598044"
---
### <a name="ca1417-outattribute-on-string-parameter-for-pinvoke"></a>CA1417: OutAttribute no parâmetro de cadeia de caracteres para P/Invoke

A regra do analisador de código .NET [CA1417](/visualstudio/code-quality/ca1417) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para qualquer definição de método de [invocação de plataforma (P/Invoke)](../../../../docs/standard/native-interop/pinvoke.md) , em que um <xref:System.String> parâmetro é passado por valor e marcado com <xref:System.Runtime.InteropServices.OutAttribute> .

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA1417](/visualstudio/code-quality/ca1417). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

Regra CA1417 flags [P/Invoke](../../../../docs/standard/native-interop/pinvoke.md) definições de método em que um <xref:System.String> parâmetro é marcado com o <xref:System.Runtime.InteropServices.OutAttribute> atributo e é passado por valor. Por exemplo:

```csharp
[DllImport("MyLibrary")]
private static extern void PIMethod([Out] string s);
```

O tempo de execução do .NET mantém uma tabela, chamada de pool do estagiário, que contém uma única referência a cada cadeia de caracteres literal exclusiva em um programa. Se uma cadeia de caracteres do InterNIC marcada com <xref:System.Runtime.InteropServices.OutAttribute> for passada por valor para um método P/Invoke, o tempo de execução poderá ser desestabilizado. Para obter mais informações sobre o InterNIC da cadeia de caracteres, consulte comentários para <xref:System.String.Intern(System.String)?displayProperty=nameWithType> .

#### <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

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

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).

#### <a name="category"></a>Categoria

Análise de código

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
