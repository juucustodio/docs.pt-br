---
title: 'Alteração significativa: IntPtr e UIntPtr implementam IFormattable'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que IntPtr e UIntPtr agora implementam IFormattable.
ms.date: 11/01/2020
ms.openlocfilehash: 0684652cdc2b8cf1d237074263bf0809082b0dcd
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760506"
---
# <a name="intptr-and-uintptr-implement-iformattable"></a>IntPtr e UIntPtr implementam IFormattable

<xref:System.IntPtr> e <xref:System.UIntPtr> agora implemente <xref:System.IFormattable> . As funções que verificam o <xref:System.IFormattable> suporte agora podem retornar resultados diferentes para esses tipos, pois eles podem passar um especificador de formato e uma cultura.

## <a name="change-description"></a>Descrição das alterações

Em versões anteriores do .NET, <xref:System.IntPtr> e <xref:System.UIntPtr> não implemente <xref:System.IFormattable> . As funções que verificam <xref:System.IFormattable> podem retornar a apenas chamar <xref:System.IntPtr.ToString%2A?displayProperty=nameWithType> ou <xref:System.UIntPtr.ToString%2A?displayProperty=nameWithType> , o que significa que especificadores de formato e culturas não são respeitados.

No .NET 5,0 e versões posteriores, <xref:System.IntPtr> e <xref:System.UIntPtr> implemente <xref:System.IFormattable> . As funções que verificam o <xref:System.IFormattable> suporte agora podem retornar resultados diferentes para esses tipos, pois eles podem passar um especificador de formato e uma cultura.

Essa alteração afeta cenários como cadeias de caracteres interpoladas e <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> , entre outros.

## <a name="reason-for-change"></a>Motivo da alteração

<xref:System.IntPtr> e <xref:System.UIntPtr> agora tem suporte a idiomas em C# por meio das `nint` `nuint` palavras-chave e. Os tipos de suporte foram atualizados para fornecer paridade próxima (quando possível) com a funcionalidade exposta por outros tipos primitivos, como <xref:System.Int32?displayProperty=nameWithType> .

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Se você não quiser que um especificador de formato ou cultura personalizada seja usado ao exibir valores desses tipos, você pode chamar o <xref:System.IntPtr.ToString?displayProperty=nameWithType> e <xref:System.UIntPtr.ToString?displayProperty=nameWithType> sobrecargas de `ToString()` .

## <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

### Category

Core .NET libraries

### Affected APIs

Not detectable via API analysis.

-->
