---
title: 'Alteração significativa: DataGridView não redefine mais as fontes para estilos de célula personalizados'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que DataGridView não redefine mais as fontes de estilo de célula padrão para corresponder à fonte de ambiente se a fonte de estilo de célula tiver sido personalizada.
ms.date: 10/18/2020
ms.openlocfilehash: 708b12ba1305681f5c38eb605861d02e3b2c8eb1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760545"
---
# <a name="datagridview-no-longer-resets-fonts-for-customized-cell-styles"></a>DataGridView não redefine mais as fontes para estilos de célula personalizados

Quando a fonte de ambiente for alterada, o <xref:System.Windows.Forms.DataGridViewElement.DataGridView> não redefinirá mais as fontes de estilo de célula padrão para corresponder à fonte de ambiente se a fonte de estilo de célula tiver sido personalizada.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, se a fonte do ambiente mudar, o <xref:System.Windows.Forms.DataGridViewElement.DataGridView> redefinirá e substituirá as fontes definidas pelo usuário nas <xref:System.Windows.Forms.DataGridView.DefaultCellStyle> <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> Propriedades, e <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> .

A partir do .NET 5,0, se você definir as configurações de fonte nas <xref:System.Windows.Forms.DataGridView.DefaultCellStyle> <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> Propriedades,, ou <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> , essas configurações serão mantidas mesmo quando a fonte do ambiente for alterada. Para qualquer uma dessas propriedades que você não personalize a fonte, a fonte será alterada para corresponder às configurações de fonte do ambiente.

## <a name="reason-for-change"></a>Motivo da alteração

Com a [alteração da fonte padrão no .NET Core 3,0](../../winforms.md#default-control-font-changed-to-segoe-ui-9-pt), as configurações de fonte padrão para os vários estilos de célula também foram alteradas. Esse comportamento não é desejável para aplicativos que dependem de estilo personalizado em seus <xref:System.Windows.Forms.DataGridViewElement.DataGridView> controles e impedia a migração desses aplicativos de .NET Framework para o .net 5,0.

## <a name="version-introduced"></a>Versão introduzida

.NET 5,0

## <a name="recommended-action"></a>Ação recomendada

Nenhuma ação é necessária em sua parte. No entanto, se você personalizou a fonte <xref:System.Windows.Forms.DataGridView.DefaultCellStyle> nas <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> Propriedades,, ou <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> e quiser que a fonte corresponda à fonte de ambiente, defina <xref:System.Windows.Forms.DataGridViewCellStyle.Font?displayProperty=nameWithType> como `null` para cada propriedade.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle?displayProperty=fullName>

<!--

### Affected APIs

- `P:System.Windows.Forms.DataGridView.DefaultCellStyle`
- `P:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle`
- `P:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle`

### Category

- Windows Forms

-->
