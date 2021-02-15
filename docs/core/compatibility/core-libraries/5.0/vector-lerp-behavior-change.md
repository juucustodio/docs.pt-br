---
title: 'Alteração significativa: alteração de comportamento para vector2. Lerp e Vector4. Lerp'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que a implementação de vector2. Lerp e Vector4. Lerp mudou para uma conta correta para um erro de arredondamento de ponto flutuante.
ms.date: 11/01/2020
ms.openlocfilehash: 8e363a559dba8b7563c40637c47f101d59951216
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760343"
---
# <a name="behavior-change-for-vector2lerp-and-vector4lerp"></a>Alteração de comportamento para vector2. Lerp e Vector4. Lerp

A implementação de <xref:System.Numerics.Vector2.Lerp(System.Numerics.Vector2,System.Numerics.Vector2,System.Single)?displayProperty=nameWithType> e <xref:System.Numerics.Vector4.Lerp(System.Numerics.Vector4,System.Numerics.Vector4,System.Single)?displayProperty=nameWithType> mudou para uma conta correta para um erro de arredondamento de ponto flutuante.

## <a name="change-description"></a>Descrição das alterações

Anteriormente, <xref:System.Numerics.Vector2.Lerp(System.Numerics.Vector2,System.Numerics.Vector2,System.Single)?displayProperty=nameWithType> e <xref:System.Numerics.Vector4.Lerp(System.Numerics.Vector4,System.Numerics.Vector4,System.Single)?displayProperty=nameWithType> foram implementados como `value1 + (value2 - value1) * amount` . No entanto, devido a um erro de arredondamento de ponto flutuante, esse algoritmo nem sempre retorna `value2` quando `amount` é `1.0f` .

No .NET 5,0 e posterior, a implementação usa o mesmo algoritmo que <xref:System.Numerics.Vector3.Lerp(System.Numerics.Vector3,System.Numerics.Vector3,System.Single)?displayProperty=nameWithType> , que é `(value1 * (1.0f - amount)) + (value2 * amount)` . Esse algoritmo conta corretamente para o erro de arredondamento. Agora, quando `amount` é `1.0f` , o resultado é precisamente `value2` . O algoritmo atualizado também permite que o algoritmo seja otimizado livremente usando <xref:System.MathF.FusedMultiplyAdd%2A?displayProperty=nameWithType> quando ele está disponível.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Nenhuma ação é necessária. No entanto, se você quiser manter o comportamento antigo, poderá implementar sua própria `Lerp` função que usa o algoritmo anterior do `value1 + (value2 - value1) * amount` .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Numerics.Vector2.Lerp(System.Numerics.Vector2,System.Numerics.Vector2,System.Single)?displayProperty=fullName>
- <xref:System.Numerics.Vector4.Lerp(System.Numerics.Vector4,System.Numerics.Vector4,System.Single)?displayProperty=fullName>

<!--

#### Category

Core .NET libraries

### Affected APIs

- `M:System.Numerics.Vector2.Lerp(System.Numerics.Vector2,System.Numerics.Vector2,System.Single)`
- `M:System.Numerics.Vector4.Lerp(System.Numerics.Vector4,System.Numerics.Vector4,System.Single)`

-->
