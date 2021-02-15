---
title: 'Alteração significativa: verificações IsSupported de hardware intrínsecas podem diferir para tipos aninhados'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que a verificação de x64. Issupportd para intrínsecos de hardware agora pode produzir um resultado diferente.
ms.date: 11/01/2020
ms.openlocfilehash: 9acef15860de76a9743621cb4c5edba5aac3931c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760415"
---
# <a name="hardware-intrinsic-issupported-checks-may-differ-for-nested-types"></a>Verificações IsSupported de hardware intrínsecas podem diferir para tipos aninhados

A verificação `<Isa>.X64.IsSupported` , em que `<Isa>` se refere às classes no <xref:System.Runtime.Intrinsics.X86?displayProperty=nameWithType> namespace, agora pode produzir um resultado diferente para versões anteriores do .net.

> [!TIP]
> O *ISA* significa arquitetura padrão do setor.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, alguns dos <xref:System.Runtime.Intrinsics.X86> tipos intrínsecos a hardware, por exemplo,, <xref:System.Runtime.Intrinsics.X86.Aes?displayProperty=nameWithType> não expõevam uma `X64` classe aninhada. Para esses tipos, chamar `<Isa>.X64.IsSupported` resolvido para uma `IsSupported` propriedade em uma classe aninhada `X64` de uma classe pai de `<Isa>` . Isso significava que a propriedade poderia retornar `true` mesmo quando `<Isa>.IsSupported` retorna `false` .

No .NET 5,0 e versões posteriores, todos os <xref:System.Runtime.Intrinsics.X86> tipos expõem uma `X64` classe aninhada que relata adequadamente o suporte. Isso garante que a hierarquia geral permaneça correta e que `<Isa>.X64.IsSupported` , se for `true` , `<Isa>.IsSupported` também possa ser considerada `true` .

## <a name="reason-for-change"></a>Motivo da alteração

A intenção era que `<Isa>.X64.IsSupported` , se estiver `true` , `<Isa>.IsSupported` também esteja implícita `true` . No entanto, devido à forma como a resolução de membros funciona em C#, as classes que não tinham uma classe aninhada apresentaram `X64` uma situação em que isso não era sempre o caso e levou a bugs no código do usuário.

## <a name="recommended-action"></a>Ação recomendada

Se necessário, ajuste o código que verifica `IsSupported` para verificar o ISA apropriado.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.Intrinsics.X86.Aes.X64.IsSupported?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Avx.X64.IsSupported?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Avx2.X64.IsSupported?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Fma.X64.IsSupported?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Pclmulqdq.X64.IsSupported?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse3.X64.IsSupported?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Ssse3.X64.IsSupported?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `P:System.Runtime.Intrinsics.X86.Aes.X64.IsSupported`
- `P:System.Runtime.Intrinsics.X86.Avx.X64.IsSupported`
- `P:System.Runtime.Intrinsics.X86.Avx2.X64.IsSupported`
- `P:System.Runtime.Intrinsics.X86.Fma.X64.IsSupported`
- `P:System.Runtime.Intrinsics.X86.Pclmulqdq.X64.IsSupported`
- `P:System.Runtime.Intrinsics.X86.Sse3.X64.IsSupported`
- `P:System.Runtime.Intrinsics.X86.Ssse3.X64.IsSupported`

-->
