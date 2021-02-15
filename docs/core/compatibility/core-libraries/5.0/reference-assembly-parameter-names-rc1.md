---
title: 'Alteração significativa: nomes de parâmetros alterados no RC2'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET, em que alguns nomes de parâmetro do assembly de referência foram alterados nas versões Preview e Release-Candidate do .NET 5,0.
ms.date: 11/01/2020
ms.openlocfilehash: 554a4fa9e08fdb504f380465496d7e7e9df85814
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760389"
---
# <a name="parameter-names-changed-in-rc2"></a>Nomes de parâmetros alterados no RC2

Alguns nomes de parâmetro de assembly de referência foram alterados para corresponder nomes de parâmetro nos assemblies de implementação.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET 5,0 Preview e RC, alguns nomes de parâmetros de [assembly de referência](../../../../standard/assembly/reference-assemblies.md) são diferentes para seus parâmetros correspondentes no assembly de implementação. Isso pode causar problemas ao usar argumentos nomeados e reflexão.

No .NET 5,0 RC2, esses nomes de parâmetro incompatíveis foram atualizados nos assemblies de referência para corresponder exatamente aos nomes de parâmetro correspondentes nos assemblies de implementação.

A tabela a seguir mostra as APIs e os nomes de parâmetro que foram alterados.

| API | Nome do parâmetro antigo | Nome do novo parâmetro |
| - | - | - |
| <xref:System.Diagnostics.ActivityContext.%23ctor(System.Diagnostics.ActivityTraceId,System.Diagnostics.ActivitySpanId,System.Diagnostics.ActivityTraceFlags,System.String,System.Boolean)> | `traceOptions` | `traceFlags` |
| <xref:System.Globalization.CompareInfo.IsPrefix(System.ReadOnlySpan{System.Char},System.ReadOnlySpan{System.Char},System.Globalization.CompareOptions,System.Int32@)?displayProperty=nameWithType> | `suffix` | `prefix` |

## <a name="reason-for-change"></a>Motivo da alteração

Os nomes de parâmetro foram alterados quanto à consistência e para evitar falhas ao usar argumentos nomeados e reflexão.

## <a name="version-introduced"></a>Versão introduzida

5,0 RC2

## <a name="recommended-action"></a>Ação recomendada

Se você encontrar um erro de compilador devido a uma alteração de nome de parâmetro, atualize o nome do parâmetro de acordo.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Diagnostics.ActivityContext.%23ctor(System.Diagnostics.ActivityTraceId,System.Diagnostics.ActivitySpanId,System.Diagnostics.ActivityTraceFlags,System.String,System.Boolean)>
- <xref:System.Globalization.CompareInfo.IsPrefix(System.ReadOnlySpan{System.Char},System.ReadOnlySpan{System.Char},System.Globalization.CompareOptions,System.Int32@)?displayProperty=fullName>

<!--

#### Category

Core .NET libraries

### Affected APIs

- `M:System.Diagnostics.ActivityContext.#ctor(System.Diagnostics.ActivityTraceId,System.Diagnostics.ActivitySpanId,System.Diagnostics.ActivityTraceFlags,System.String,System.Boolean)`
- `M:System.Globalization.CompareInfo.IsPrefix(System.ReadOnlySpan{System.Char},System.ReadOnlySpan{System.Char},System.Globalization.CompareOptions,System.Int32@)`

-->
