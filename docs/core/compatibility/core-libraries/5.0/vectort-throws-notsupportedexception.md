---
title: 'Alteração significativa: vetor <T> gera NotSupportedException'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que <T> o vetor sempre gera uma exceção para parâmetros de tipo sem suporte.
ms.date: 11/01/2020
ms.openlocfilehash: 63db7c6b720735b180ed11098227b31a14008f74
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760396"
---
# <a name="vectort-always-throws-notsupportedexception-for-unsupported-types"></a>Vetor \<T> sempre gera NotSupportedException para tipos sem suporte

<xref:System.Numerics.Vector%601?displayProperty=nameWithType> Agora sempre gera um <xref:System.NotSupportedException> para parâmetros de tipo sem suporte.

## <a name="change-description"></a>Descrição das alterações

Anteriormente, os membros de <xref:System.Numerics.Vector%601> nem sempre geraram um <xref:System.NotSupportedException> quando `T` era um [tipo sem suporte](#unsupported-types). A exceção nem sempre foi acionada devido a caminhos de código com suporte para aceleração de hardware. Por exemplo, `Vector<bool> + Vector<bool>` retornado `default` em vez de lançar uma exceção em plataformas que não têm aceleração de hardware, como ARM32. Para tipos sem suporte, <xref:System.Numerics.Vector%601> os membros exibiram comportamento inconsistente em diferentes plataformas e configurações de hardware.

A partir do .NET 5,0, <xref:System.Numerics.Vector%601> os membros sempre lançam um <xref:System.NotSupportedException> em todas as configurações de hardware quando `T` não é um tipo com suporte.

### <a name="unsupported-types"></a>Tipos sem suporte

Os tipos com suporte para o parâmetro de tipo de <xref:System.Numerics.Vector%601> são:

- `byte`
- `sbyte`
- `short`
- `ushort`
- `int`
- `uint`
- `long`
- `ulong`
- `float`
- `double`

Os tipos com suporte não foram alterados, no entanto, eles podem ser alterados no futuro.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Não use um tipo sem suporte para o parâmetro de tipo de <xref:System.Numerics.Vector%601> .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Numerics.Vector%601?displayProperty=fullName> e todos os seus membros

<!--

#### Category

Core .NET libraries

### Affected APIs

- ``T:System.Numerics.Vector`1``

-->
