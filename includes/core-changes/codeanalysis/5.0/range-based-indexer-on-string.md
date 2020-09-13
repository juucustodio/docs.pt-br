---
ms.openlocfilehash: 4e937f56f6315ce2abf76dd56989f4d2c4059f22
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598056"
---
### <a name="ca1831-use-asspan-instead-of-range-based-indexers-for-string"></a>CA1831: usar asspan em vez de indexadores baseados em intervalo para cadeia de caracteres

A regra do analisador de código .NET [CA1831](/visualstudio/code-quality/ca1831) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para qualquer código em que um <xref:System.Range> indexador baseado em um é usado em uma cadeia de caracteres, mas nenhuma cópia foi pretendida.

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA1831](/visualstudio/code-quality/ca1831). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

A regra CA1831 localiza instâncias em que o <xref:System.Range> indexador baseado em um é usado em uma cadeia de caracteres, mas nenhuma cópia foi pretendida. Se o <xref:System.Range> indexador baseado for usado diretamente em uma cadeia de caracteres para produzir uma conversão implícita, uma cópia desnecessária da parte solicitada da cadeia de caracteres será criada. Por exemplo:

```csharp
ReadOnlySpan<char> slice = str[1..3];
```

O CA1831 sugere o uso do <xref:System.Range> indexador baseado em um *intervalo* da cadeia de caracteres, em vez disso. Por exemplo:

```csharp
ReadOnlySpan<char> slice = str.AsSpan()[1..3];
```

#### <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

- Para corrigir seu código e evitar alocações desnecessárias, chame <xref:System.MemoryExtensions.AsSpan(System.String)> ou <xref:System.MemoryExtensions.AsMemory(System.String)> antes de usar o <xref:System.Range> indexador baseado em. Por exemplo:

  ```csharp
  ReadOnlySpan<char> slice = str.AsSpan()[1..3];
  ```

- Se você não quiser alterar seu código, poderá desabilitar a regra definindo sua severidade como `suggestion` ou `none` . Para obter mais informações, consulte [configurar regras de análise de código](../../../../docs/fundamentals/productivity/configure-code-analysis-rules.md).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).

#### <a name="category"></a>Categoria

Análise de código

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Range?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Range`

-->
