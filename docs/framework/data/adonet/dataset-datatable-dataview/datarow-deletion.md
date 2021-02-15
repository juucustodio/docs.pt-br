---
description: 'Saiba mais sobre: exclusão de DataRow'
title: Exclusão de DataRow
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c34f531d-4b9b-4071-b2d7-342c402aa586
ms.openlocfilehash: fff3117256629c2fa0262e2aa163da09174390dc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739567"
---
# <a name="datarow-deletion"></a>Exclusão de DataRow

Há dois métodos que você pode usar para excluir um <xref:System.Data.DataRow> objeto de um <xref:System.Data.DataTable> objeto: o método **Remove** do <xref:System.Data.DataRowCollection> objeto e o <xref:System.Data.DataRow.Delete%2A> método do objeto **DataRow** . Enquanto o <xref:System.Data.DataRowCollection.Remove%2A> método exclui uma **DataRow** de **DataRowCollection**, o <xref:System.Data.DataRow.Delete%2A> método marca apenas a linha para exclusão. A remoção real ocorre quando o aplicativo chama o método **AcceptChanges** . Usando <xref:System.Data.DataRow.Delete%2A>, você pode verificar programaticamente quais linhas estão marcadas para exclusão antes de realmente removê-las. Quando uma linha está marcada para exclusão, sua propriedade <xref:System.Data.DataRow.RowState%2A> é definida como <xref:System.Data.DataRow.Delete%2A>.  
  
 Nem <xref:System.Data.DataRow.Delete%2A> ou <xref:System.Data.DataRowCollection.Remove%2A> deve ser chamado em um loop foreach ao fazer a iteração por meio de um objeto de <xref:System.Data.DataRowCollection>. Nem <xref:System.Data.DataRow.Delete%2A> ou <xref:System.Data.DataRowCollection.Remove%2A> modificam o estado da coleção.  
  
 Ao usar uma <xref:System.Data.DataSet> **DataTable** ou em conjunto com um **DataAdapter** e uma fonte de dados relacional, use o método **delete** da **DataRow** para remover a linha. O método **delete** marca a linha como **excluída** no **DataSet** ou **DataTable** , mas não a remove. Em vez disso, quando o **DataAdapter** encontra uma linha marcada como **excluída**, ele executa seu método **DeleteCommand** para excluir a linha na fonte de dados. Em seguida, a linha pode ser removida permanentemente usando o método **AcceptChanges** . Se você usar **remover** para excluir a linha, a linha será completamente removida da tabela, mas o **DataAdapter** não excluirá a linha na fonte de dados.  
  
 O método **Remove** da **DataRowCollection** usa uma **DataRow** como um argumento e a remove da coleção, conforme mostrado no exemplo a seguir.  
  
```vb  
workTable.Rows.Remove(workRow)  
```  
  
```csharp  
workTable.Rows.Remove(workRow);  
```  
  
 Por outro lado, o exemplo a seguir demonstra como chamar o método **delete** em uma **DataRow** para alterar seu **RowState** para **excluído**.  
  
```vb  
workRow.Delete  
```  
  
```csharp  
workRow.Delete();  
```  
  
 Se uma linha for marcada para exclusão e você chamar o método **AcceptChanges** do objeto **DataTable** , a linha será removida da **DataTable**. Por outro lado, se você chamar **RejectChanges**, o **RowState** da linha será revertido para o que estava antes de ser marcado como **excluído**.  
  
> [!NOTE]
> Se o **RowState** de uma **DataRow** for **adicionado**, o que significa que acabou de ser adicionado à tabela e, em seguida, marcado como **excluído**, ele será removido da tabela.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataRow>
- <xref:System.Data.DataRowCollection>
- <xref:System.Data.DataTable>
- [Manipulando dados em uma DataTable](manipulating-data-in-a-datatable.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
