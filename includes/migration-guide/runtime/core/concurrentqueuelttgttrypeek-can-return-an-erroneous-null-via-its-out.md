---
ms.openlocfilehash: 004e2d1883b631e88ab5e164b1120c3b081b7041
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497645"
---
### <a name="concurrentqueuelttgttrypeek-can-return-an-erroneous-null-via-its-out-parameter"></a>ConcurrentQueue&lt;T&gt;.TryPeek pode retornar um nulo errado por meio de seus parâmetros de saída

#### <a name="details"></a>Detalhes

Em alguns cenários multithread, <xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=fullName> pode retornar true, mas popular o parâmetro de saída com um valor nulo (em vez do valor correto, inspecionado).

#### <a name="suggestion"></a>Sugestão

Esse problema foi corrigido no .NET Framework 4.5.1. O upgrade para esse Framework resolverá o problema.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Principal|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=nameWithType>

<!--

#### Affected APIs

- ``M:System.Collections.Concurrent.ConcurrentQueue`1.TryPeek(`0@)``

-->
