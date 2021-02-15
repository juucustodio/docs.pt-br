---
title: 'Alteração significativa: os métodos SSE e SSE2 CompareGreaterThan manipulam corretamente as entradas NaN'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que os métodos de comparação SSE e SSE2 foram corrigidos para lidar corretamente com entradas NaN.
ms.date: 11/01/2020
ms.openlocfilehash: 4abffa8d8bf2abfa9ef83673db9154de035d952c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760332"
---
# <a name="sse-and-sse2-comparegreaterthan-methods-properly-handle-nan-inputs"></a>Os métodos SSE e SSE2 CompareGreaterThan manipulam corretamente as entradas NaN

Os métodos e a seguir foram <xref:System.Runtime.Intrinsics.X86.Sse?displayProperty=nameWithType> <xref:System.Runtime.Intrinsics.X86.Sse2?displayProperty=nameWithType> corrigidos para lidar corretamente com `NaN` entradas e corresponder ao comportamento de hardware dos métodos equivalentes na <xref:System.Runtime.Intrinsics.X86.Avx?displayProperty=nameWithType> classe:

* `CompareGreaterThan`
* `CompareGreaterThanOrEqual`
* `CompareNotGreaterThan`
* `CompareNotGreaterThanOrEqual`
* `CompareScalarGreaterThan`
* `CompareScalarGreaterThanOrEqual`
* `CompareScalarNotGreaterThan`
* `CompareScalarNotGreaterThanOrEqual`

## <a name="change-description"></a>Descrição das alterações

Anteriormente, `NaN` as entradas para os <xref:System.Runtime.Intrinsics.X86.Sse> métodos listados e <xref:System.Runtime.Intrinsics.X86.Sse2> retornaram um resultado incorreto. O resultado também é diferente do resultado gerado pelo método correspondente na <xref:System.Runtime.Intrinsics.X86.Avx> classe.

A partir do .NET 5,0, esses métodos manipulam corretamente `NaN` as entradas e retornam os mesmos resultados que os métodos correspondentes na <xref:System.Runtime.Intrinsics.X86.Avx> classe.

As arquiteturas de Streaming SIMD Extensions (SSE) e Streaming SIMD Extensions 2 (SSE2) do setor (ISAs) não fornecem suporte direto de hardware para esses métodos de comparação, para que sejam implementadas no software. Anteriormente, os métodos foram implementados incorretamente e eles incorretamente manipulavam `NaN` entradas. Para o código portado de nativo, o comportamento incorreto pode introduzir bugs. Para um caminho de código de 256 bits, os métodos também podem produzir resultados diferentes para os métodos equivalentes na <xref:System.Runtime.Intrinsics.X86.Avx> classe.

Como exemplo de como os métodos estavam incorretos anteriormente, você pode implementar `CompareNotGreaterThan(x,y)` como `CompareLessThanOrEqual(x,y)` para inteiros regulares. No entanto, para `NaN` entradas, essa lógica computa o resultado errado. Em vez disso, usar `CompareNotLessThan(y,x)` compara os números corretamente *e* leva as `NaN` entradas em consideração.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- Se o comportamento anterior era um bug, nenhuma alteração é necessária.

- Se o comportamento anterior foi desejado, você pode manter esse comportamento alterando a invocação relevante da seguinte maneira:

  * `CompareGreaterThan(x,y)` -> `CompareNotLessThanOrEqual(x,y)`
  * `CompareGreaterThanOrEqual(x,y)` -> `CompareNotLessThan(x,y)`
  * `CompareNotGreaterThan(x,y)` -> `CompareLessThanOrEqual(x,y)`
  * `CompareNotGreaterThanOrEqual(x,y)` -> `CompareLessThan(x,y)`
  * `CompareScalarGreaterThan(x,y)` -> `CompareScalarNotLessThanOrEqual(x,y)`
  * `CompareScalarGreaterThanOrEqual(x,y)` -> `CompareScalarNotLessThan(x,y)`
  * `CompareScalarNotGreaterThan(x,y)` -> `CompareScalarLessThanOrEqual(x,y)`
  * `CompareScalarNotGreaterThanOrEqual(x,y)` -> `CompareScalarLessThan(x,y)`

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>

- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>

<!--

#### Category

Core .NET libraries

### Affected APIs

- `M:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`

- `M:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`

-->
