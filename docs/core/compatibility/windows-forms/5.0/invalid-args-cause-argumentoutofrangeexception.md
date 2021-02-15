---
title: 'Alteração significativa: as propriedades do WinForms agora lançam ArgumentOutOfRangeException'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que algumas propriedades de Windows Forms agora lançam um ArgumentOutOfRangeException para argumentos inválidos.
ms.date: 06/18/2020
ms.openlocfilehash: 94593047d16304ce401b23993ad4ca173c10812b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760479"
---
# <a name="winforms-properties-now-throw-argumentoutofrangeexception"></a>As propriedades do WinForms agora geram ArgumentOutOfRangeException

Algumas propriedades de Windows Forms agora lançam um <xref:System.ArgumentOutOfRangeException> para argumentos inválidos, onde anteriormente não.

## <a name="change-description"></a>Descrição das alterações

Anteriormente, essas propriedades lançavam várias exceções, como <xref:System.NullReferenceException> , <xref:System.IndexOutOfRangeException> ou, <xref:System.ArgumentException> quando passaram argumentos fora do intervalo. A partir do .NET 5,0, essas propriedades agora lançam <xref:System.ArgumentOutOfRangeException> argumentos When passados que estão fora do intervalo.

Lançar um <xref:System.ArgumentOutOfRangeException> está em conformidade com o comportamento do tempo de execução do .net. Ele também melhora a experiência de depuração ao comunicar-se claramente qual argumento é inválido.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

- Atualize o código para evitar a passagem de argumentos inválidos.
- Se necessário, manipule um <xref:System.ArgumentOutOfRangeException> ao definir a propriedade.

## <a name="affected-apis"></a>APIs afetadas

A tabela a seguir lista as propriedades e os parâmetros afetados:

> [!div class="mx-tdBreakAll"]
> | Propriedade | Nome do parâmetro | Versão adicionada |
> |-|-|-|
> | <xref:System.Windows.Forms.ListBox.IntegerCollection.Item(System.Int32)?displayProperty=nameWithType> | `index` | 5,0 Preview 5 |
> | <xref:System.Windows.Forms.TreeNode.ImageIndex?displayProperty=nameWithType> | `value` | 5,0 Preview 6 |
> | <xref:System.Windows.Forms.TreeNode.SelectedImageIndex?displayProperty=nameWithType> | `value` | 5,0 Preview 6 |

<!--

### Affected APIs

- `P:System.Windows.Forms.ListBox.IntegerCollection.Item(System.Int32)`
- `P:System.Windows.Forms.TreeNode.ImageIndex`
- `P:System.Windows.Forms.TreeNode.SelectedImageIndex`

### Category

Windows Forms

-->
