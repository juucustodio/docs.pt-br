---
title: 'Alteração significativa: reconhecimento de URI de caminhos UNC no UNIX'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que a classe Uri agora reconhece cadeias de caracteres que começam com duas barras invertidas como caminhos UNC no UNIX.
ms.date: 11/01/2020
ms.openlocfilehash: 0d5d9cd8dd869f24e94d15724e5e16eaddf6ed47
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760331"
---
# <a name="uri-recognition-of-unc-paths-on-unix"></a>Reconhecimento de URI de caminhos UNC no UNIX

A <xref:System.Uri> classe agora reconhece cadeias de caracteres que começam com duas barras ( `//` ) como caminhos UNC (Convenção de nomenclatura universal) em sistemas operacionais UNIX. Essa alteração torna o comportamento de tais cadeias de caracteres consistentes em todas as plataformas.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, a <xref:System.Uri> classe reconhece cadeias de caracteres que começam com duas barras "/", por exemplo, `//contoso` como caminhos de arquivo absolutos em sistemas operacionais UNIX. No entanto, no Windows, essas cadeias de caracteres são reconhecidas como caminhos UNC.

A partir do .NET 5,0, a <xref:System.Uri> classe reconhece cadeias de caracteres que começam com duas barras invertidas como caminhos UNC em todas as plataformas, incluindo UNIX. Além disso, as propriedades se comportam de acordo com a semântica UNC:

- <xref:System.Uri.IsUnc?displayProperty=nameWithType> retorna `true`.
- As barras invertidas no caminho são substituídas por barras "/". Por exemplo, `//first\second` torna-se `//first/second`.
- <xref:System.Uri.LocalPath?displayProperty=nameWithType> Não codificar caracteres por porcentagem. Por exemplo, `//first/\uFFF0` *não* é convertido em `//first/%EF%BF%B0` .

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Nenhuma ação é necessária na parte do desenvolvedor.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Uri?displayProperty=fullName>

<!--

#### Category

Core .NET libraries

### Affected APIs

- `T:System.Uri`

-->
