---
title: 'Alteração significativa: caminhos de URI com caracteres não ASCII são analisados corretamente no UNIX'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que caminhos de URI absolutos que contêm caracteres não ASCII agora são analisados corretamente em plataformas UNIX.
ms.date: 11/01/2020
ms.openlocfilehash: 94de4e0eb94a11153d873871d4003422a4286a0c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760326"
---
# <a name="uri-paths-with-non-ascii-characters-parse-correctly-on-unix"></a>Caminhos de URI com caracteres não ASCII são analisados corretamente no UNIX

Um bug foi corrigido na <xref:System.Uri?displayProperty=fullName> classe, de modo que os caminhos de URI absolutos que contêm caracteres não-ASCII agora são analisados corretamente em plataformas UNIX.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, caminhos de URI absolutos que contêm caracteres não ASCII são analisados incorretamente em plataformas UNIX e os segmentos do caminho são duplicados. (Caminhos absolutos são aqueles que começam com "/".) O problema de análise foi corrigido para o .NET 5,0. Se você mudar de uma versão anterior do .NET para o .NET 5,0 ou posterior, você obterá valores diferentes produzidos por <xref:System.Uri.AbsoluteUri?displayProperty=nameWithType> , <xref:System.Uri.ToString?displayProperty=nameWithType> e outros <xref:System.Uri> Membros.

Considere a saída do código a seguir quando executada no UNIX.

```csharp
var myUri = new Uri("/üri");

Console.WriteLine($"AbsoluteUri: {myUri.AbsoluteUri}");
Console.WriteLine($"ToString: {myUri.ToString()}");
```

Saída na versão anterior do .NET:

```text
AbsoluteUri: /%C3%BCri/%C3%BCri
ToString: /üri/üri
```

Saída no .NET 5,0 ou versão posterior:

```text
AbsoluteUri: /%C3%BCri
ToString: /üri
```

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Se você tiver um código que espera e contas para os segmentos de caminho duplicados, você pode remover esse código.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Uri?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `T:System.Uri`

-->
