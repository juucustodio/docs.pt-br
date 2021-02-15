---
title: 'Alteração significativa: TextFormatFlags. Modifystring é obsoleto'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que o campo TextFormatFlags. Modifystring está obsoleto como um aviso.
ms.date: 11/05/2020
ms.openlocfilehash: 83dca65a770ccdcd5ce48bb669f5122dc2d5ad77
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760352"
---
# <a name="textformatflagsmodifystring-is-obsolete"></a>TextFormatFlags. Modifystring é obsoleto

O <xref:System.Windows.Forms.TextFormatFlags.ModifyString?displayProperty=nameWithType> campo é obsoleto, como um aviso, e pode ser removido em uma versão futura do .net.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, o <xref:System.Windows.Forms.TextFormatFlags.ModifyString?displayProperty=nameWithType> campo de enumeração não está marcado como obsoleto. No .NET 5,0 e versões posteriores, ele é marcado como obsoleto como um aviso. Esse campo pode ser removido em uma versão futura do .NET.

## <a name="reason-for-change"></a>Motivo da alteração

Passar uma cadeia de caracteres para <xref:System.Windows.Forms.TextRenderer.MeasureText%2A?displayProperty=nameWithType> com <xref:System.Windows.Forms.TextFormatFlags.ModifyString?displayProperty=nameWithType> altera a cadeia de caracteres em algumas situações. Esse comportamento interrompe a promessa de imutabilidade da cadeia de caracteres e pode levar a uma corrupção fatal do estado do tempo de execução .NET.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

Atualize qualquer código que dependa de <xref:System.Windows.Forms.TextFormatFlags.ModifyString?displayProperty=nameWithType> .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Forms.TextFormatFlags.ModifyString?displayProperty=fullName>

<!--

### Affected APIs

- `F:System.Windows.Forms.TextFormatFlags.ModifyString`

### Category

Windows Forms

-->
