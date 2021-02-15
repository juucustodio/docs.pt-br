---
title: 'Alteração significativa: MulticastOption. Group não aceita um valor nulo'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que MulticastOption. Group não aceita mais um valor nulo.
ms.date: 08/18/2020
ms.openlocfilehash: 164ac8c2c8dd14f9e0758017e54eeb377f88a7e5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760357"
---
# <a name="multicastoptiongroup-doesnt-accept-a-null-value"></a>MulticastOption. Group não aceita um valor nulo

<xref:System.Net.Sockets.MulticastOption.Group?displayProperty=nameWithType> Não aceita mais um valor de `null` . Se você definir a propriedade como `null` , um <xref:System.ArgumentNullException> será gerado.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, você pode definir a <xref:System.Net.Sockets.MulticastOption.Group?displayProperty=nameWithType> propriedade como `null` . Se o <xref:System.Net.Sockets.MulticastOption> for passado posteriormente para <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=nameWithType> , o tempo de execução lançará um <xref:System.NullReferenceException> .

No .NET 5,0 e posterior, um <xref:System.ArgumentNullException> será gerado se você definir a propriedade como `null` .

## <a name="reason-for-change"></a>Motivo da alteração

Para ser consistente com as diretrizes de design de estrutura, a propriedade foi atualizada para lançar um <xref:System.ArgumentNullException> se o valor for `null` .

## <a name="recommended-action"></a>Ação recomendada

Certifique-se de que você não definiu <xref:System.Net.Sockets.MulticastOption.Group?displayProperty=nameWithType> como `null` .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Net.Sockets.MulticastOption.Group?displayProperty=fullName>

<!--

### Affected APIs

- `P:System.Net.Sockets.MulticastOption.Group`

### Category

Networking

-->
