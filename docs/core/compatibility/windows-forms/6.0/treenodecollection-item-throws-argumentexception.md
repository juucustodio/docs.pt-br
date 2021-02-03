---
title: 'Alteração significativa: TreeNodecollection. Item (Int32) gera ArgumentException para o nó em uso'
description: Saiba mais sobre a alteração significativa no .NET 6,0 em que TreeNodecollection. Item (Int32) agora gera uma ArgumentException se o nó que está sendo atribuído já estiver atribuído a um TreeView.
ms.date: 01/19/2021
ms.openlocfilehash: efd6ca5d594b2aa64e10cce2cef6c0e1c411bb1e
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506543"
---
# <a name="treenodecollectionitem-throws-exception-if-node-is-assigned-elsewhere"></a>TreeNodecollection. Item gera uma exceção se o nó for atribuído em outro lugar

<xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=nameWithType> gera um <xref:System.ArgumentException> se o nó que está sendo atribuído já estiver associado a outro <xref:System.Windows.Forms.TreeView> ou a ele <xref:System.Windows.Forms.TreeView> em um índice diferente.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, você pode atribuir um nó de árvore a uma coleção, mesmo que já esteja associado a um <xref:System.Windows.Forms.TreeView> . Isso pode levar a nós duplicados. A partir do .NET 6,0, <xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=nameWithType> o lançará um <xref:System.ArgumentException> se o nó que está sendo atribuído já estiver associado a outro <xref:System.Windows.Forms.TreeView> ou a isso <xref:System.Windows.Forms.TreeView> em um índice diferente.

## <a name="reason-for-change"></a>Motivo da alteração

Validar o parâmetro de entrada é consistente com o comportamento de outras `TreeNodeCollection` APIs.

## <a name="version-introduced"></a>Versão introduzida

.NET 6,0 Preview 1

## <a name="recommended-action"></a>Ação recomendada

Certifique-se de desassociar um `TreeNode` antes de atribuí-lo à coleção.

## <a name="affected-apis"></a>APIs afetadas

<xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=fullName>

<!--

### Affected APIs

- `P:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)`

### Category

Windows Forms

-->
