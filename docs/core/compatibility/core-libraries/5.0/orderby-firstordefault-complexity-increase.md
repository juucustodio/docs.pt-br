---
title: 'Alteração significativa: complexidade do LINQ OrderBy. primeiro {OrDefault} aumentou'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que a implementação de OrderBy. First foi alterada.
ms.date: 11/01/2020
ms.openlocfilehash: 3c4f8fd0bb2051c3e1ac14eab091be11f10f88b4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760410"
---
# <a name="complexity-of-linq-orderbyfirstordefault-increased"></a>Complexidade do LINQ OrderBy. primeiro {OrDefault} aumentou

A implementação de <xref:System.Linq.Enumerable.OrderBy%2A> `.` <xref:System.Linq.Enumerable.First%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> e <xref:System.Linq.Enumerable.OrderBy%2A> `.` <xref:System.Linq.Enumerable.FirstOrDefault%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> foi alterada, resultando em maior complexidade para a operação.

## <a name="change-description"></a>Descrição das alterações

No .NET Core 1. x-3. x, chamando <xref:System.Linq.Enumerable.OrderBy%2A> ou <xref:System.Linq.Enumerable.OrderByDescending%2A> seguido por <xref:System.Linq.Enumerable.First%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> ou <xref:System.Linq.Enumerable.FirstOrDefault%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> opera com a `O(N)` complexidade. Como apenas o primeiro elemento (ou padrão) é necessário, apenas uma enumeração é necessária para encontrá-lo. No entanto, o predicado que é fornecido para <xref:System.Linq.Enumerable.First%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> ou <xref:System.Linq.Enumerable.FirstOrDefault%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> é invocado exatamente `N` vezes, em que `N` é o comprimento da sequência.

No .NET 5,0 e versões posteriores, [foi feita uma alteração](https://github.com/dotnet/runtime/pull/36643) que chamava <xref:System.Linq.Enumerable.OrderBy%2A> ou <xref:System.Linq.Enumerable.OrderByDescending%2A> seguiu por <xref:System.Linq.Enumerable.First%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> ou <xref:System.Linq.Enumerable.FirstOrDefault%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> opera com `O(N log N)` complexidade em vez de `O(N)` complexidade. No entanto, o predicado que é fornecido para <xref:System.Linq.Enumerable.First%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> ou <xref:System.Linq.Enumerable.FirstOrDefault%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})> pode ser invocado *menos* de `N` vezes, o que é mais importante para o desempenho geral.

> [!NOTE]
> Essa alteração corresponde à implementação e à complexidade da operação no .NET Framework.

## <a name="reason-for-change"></a>Motivo da alteração

O benefício de invocar o predicado menos vezes supera uma complexidade geral mais baixa, de modo que a implementação introduzida no .NET Core 1,0 foi revertida. Para obter mais informações, consulte [este problema de dotnet/tempo de execução](https://github.com/dotnet/runtime/issues/31554).

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Nenhuma ação é necessária na parte do desenvolvedor.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=fullName>
- <xref:System.Linq.Enumerable.OrderByDescending%2A?displayProperty=fullName>
- <xref:System.Linq.Enumerable.First%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})?displayProperty=fullName>
- <xref:System.Linq.Enumerable.FirstOrDefault%60%601(System.Collections.Generic.IEnumerable{%60%600},System.Func{%60%600,System.Boolean})?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `Overload:System.Linq.Enumerable.OrderBy`
- `Overload:System.Linq.Enumerable.OrderByDescending`
- `M:System.Linq.Enumerable.First``1(System.Collections.Generic.IEnumerable{``0},System.Func{``0,System.Boolean})`
- `M:System.Linq.Enumerable.FirstOrDefault``1(System.Collections.Generic.IEnumerable{``0},System.Func{``0,System.Boolean})`

-->
