---
title: 'Alteração significativa: APIs relacionadas a DataGridView gera InvalidOperationException'
description: Saiba mais sobre a alteração significativa no .NET 5,0, em que algumas APIs relacionadas ao DataGridView lançarão uma exceção se o valor de DataGridViewCellAccessibleObject. Owner do objeto for nulo.
ms.date: 09/18/2020
ms.openlocfilehash: 927b1c9160700159a45aa1472b8d96f1a9ecfe25
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760491"
---
# <a name="datagridview-related-apis-now-throw-invalidoperationexception"></a>APIs relacionadas a DataGridView agora lança InvalidOperationException

Algumas APIs relacionadas a <xref:System.Windows.Forms.DataGridView> agora lançam um <xref:System.InvalidOperationException> se o valor do objeto <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner?displayProperty=nameWithType> for `null` .

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, as APIs afetadas lançam um <xref:System.NullReferenceException> quando são invocadas e o <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> valor é `null` . A partir do .NET 5,0, essas APIs lançam um <xref:System.InvalidOperationException> em vez de um <xref:System.NullReferenceException> se o <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> valor é `null` quando são invocados.

Lançar um <xref:System.InvalidOperationException> está em conformidade com o comportamento do tempo de execução do .net. Ele também melhora a experiência de depuração com a comunicação clara da propriedade inválida.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

Examine seu código e, se necessário, atualize-o para impedir a construção dos tipos afetados com a <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> propriedade como `null` .

## <a name="affected-apis"></a>APIs afetadas

A tabela a seguir lista as propriedades e os parâmetros afetados:

> [!div class="mx-tdBreakAll"]
> | Propriedade ou método afetado | Propriedade validada | Versão adicionada |
> |-|-|-|
> | <xref:System.Windows.Forms.DataGridViewButtonCell.DataGridViewButtonCellAccessibleObject.DoDefaultAction?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewCheckBoxCell.DataGridViewCheckBoxCellAccessibleObject.DefaultAction?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewCheckBoxCell.DataGridViewCheckBoxCellAccessibleObject.State?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewCheckBoxCell.DataGridViewCheckBoxCellAccessibleObject.DoDefaultAction?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Bounds?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.DefaultAction?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Name?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Parent?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.DoDefaultAction?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Navigate(System.Windows.Forms.AccessibleNavigation)?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewImageCell.DataGridViewImageCellAccessibleObject.DoDefaultAction?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |
> | <xref:System.Windows.Forms.DataGridViewLinkCell.DataGridViewLinkCellAccessibleObject.DoDefaultAction?displayProperty=nameWithType> | <xref:System.Windows.Forms.DataGridViewCell.DataGridViewCellAccessibleObject.Owner> | 5.0 |

<!--

### Affected APIs

- `M:System.Windows.Forms.DataGridViewButtonCell.DataGridViewButtonCellAccessibleObject.DoDefaultAction`
- `P:System.Windows.Forms.DataGridViewCheckBoxCell.DataGridViewCheckBoxCellAccessibleObject.DefaultAction`
- `P:System.Windows.Forms.DataGridViewCheckBoxCell.DataGridViewCheckBoxCellAccessibleObject.State`
- `M:System.Windows.Forms.DataGridViewCheckBoxCell.DataGridViewCheckBoxCellAccessibleObject.DoDefaultAction`
- `P:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Bounds`
- `P:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.DefaultAction`
- `P:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Name`
- `P:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Parent`
- `M:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.DoDefaultAction`
- `M:System.Windows.Forms.DataGridViewColumnHeaderCell.DataGridViewColumnHeaderCellAccessibleObject.Navigate(System.Windows.Forms.AccessibleNavigation)`
- `M:System.Windows.Forms.DataGridViewImageCell.DataGridViewImageCellAccessibleObject.DoDefaultAction`
- `M:System.Windows.Forms.DataGridViewLinkCell.DataGridViewLinkCellAccessibleObject.DoDefaultAction`

### Category

Windows Forms

-->
