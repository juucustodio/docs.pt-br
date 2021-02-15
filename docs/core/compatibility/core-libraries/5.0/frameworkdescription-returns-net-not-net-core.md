---
title: 'Alteração significativa: o valor de FrameworkDescription é .NET, em vez de .NET Core'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que RuntimeInformation. FrameworkDescription agora retorna ".NET" em vez de ".NET Core".
ms.date: 11/01/2020
ms.openlocfilehash: 3925fb092135c26291e1e60b99f359974d21553c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760417"
---
# <a name="frameworkdescriptions-value-is-net-instead-of-net-core"></a>O valor de FrameworkDescription é .NET, em vez de .NET Core

<xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> agora retorna ".NET" em vez de ".NET Core".

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> retorna ".NET Core" como parte da cadeia de caracteres de descrição, por exemplo, `.NET Core 3.1.1` .

A partir do .NET 5,0, <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> retorna ".net" como parte da cadeia de caracteres de descrição, por exemplo, `.NET 5.0.0` .

## <a name="reason-for-change"></a>Motivo da alteração

Com o .NET 5, `netcoreapp` é substituído pelo `net` como o moniker de estrutura de destino curto. Para consistência, a descrição da estrutura também foi atualizada. A alteração é superficial, pois a `FrameworkName` não é codificada em nenhum outro lugar do que na <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> propriedade.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Atualize qualquer código que pesquise ".NET Core" na cadeia de caracteres retornada por <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription> .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `P:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription`

-->
