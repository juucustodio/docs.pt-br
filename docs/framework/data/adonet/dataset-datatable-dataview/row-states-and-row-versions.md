---
description: 'Saiba mais sobre: Estados de linha e versões de linha'
title: Estados de linha e versões de linha
ms.date: 07/19/2018
dev_langs:
- csharp
- vb
ms.assetid: 2e6642c9-bfc6-425c-b3a7-e4912ffa6c1f
ms.openlocfilehash: 7d436ffcfcf59f5daa4fc6eaa9f9018b92e5c608
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651672"
---
# <a name="row-states-and-row-versions"></a>Estados de linha e versões de linha

O ADO.NET gerencia linhas nas tabelas usando estados de linha e versões. Um estado de linha indica o status de uma linha; as versões de linha mantêm os valores armazenados em uma linha à medida que são modificados, incluindo os valores atuais, originais e padrão. Por exemplo, depois que você tiver feito uma alteração em uma coluna em uma linha, a linha terá um estado de linha de `Modified` e duas versões de linha: `Current`, que contém os valores atuais de linha e `Original`, que contém os valores de linha antes que a coluna foi modificada.  
  
 Cada objeto <xref:System.Data.DataRow> tem uma propriedade <xref:System.Data.DataRow.RowState%2A> que você pode examinar para determinar o estado atual da linha. A tabela a seguir dá a você uma breve descrição de cada valor de enumeração `RowState`.  
  
|Valor de RowState|Descrição|  
|--------------------|-----------------|  
|<xref:System.Data.DataRowState.Unchanged>|Nenhuma alteração foi feita desde a última chamada para `AcceptChanges` ou desde que a linha foi criada por `DataAdapter.Fill`.|  
|<xref:System.Data.DataRowState.Added>|A linha foi adicionada à tabela, mas `AcceptChanges` não foi chamado.|  
|<xref:System.Data.DataRowState.Modified>|Algum elemento da linha foi alterado.|  
|<xref:System.Data.DataRowState.Deleted>|A linha foi excluída da tabela e `AcceptChanges` não foi chamado.|  
|<xref:System.Data.DataRowState.Detached>|A linha não faz parte de nenhum `DataRowCollection`. O `RowState` de uma linha recém-criada é definido como `Detached`. Após o novo `DataRow` ser adicionado ao `DataRowCollection` chamando o método `Add`, o valor da propriedade `RowState` é definido como `Added`.<br /><br /> `Detached` também são definidos para uma linha que foi removida de um `DataRowCollection` usando o método `Remove` ou o método `Delete` seguido pelo método `AcceptChanges`.|  
  
 Quando `AcceptChanges` tiver sido chamado em um <xref:System.Data.DataSet>, <xref:System.Data.DataTable> ou <xref:System.Data.DataRow>, todas as linhas com um estado de linha de `Deleted` serão removidas. As linhas restantes recebem um estado de linha de `Unchanged` e os valores na versão de linha `Original` são substituídos pelos valores da versão de linha `Current`. Quando `RejectChanges` tiver sido chamado, todas as linhas com um estado de `Added` serão removidas. As linhas restantes recebem um estado de linha de `Unchanged` e os valores na versão de linha `Current` são substituídos pelos valores da versão de linha `Original`.  
  
 Você pode exibir as versões de linha diferentes de uma linha passando um parâmetro <xref:System.Data.DataRowVersion> com a referência de coluna, conforme mostrado no exemplo a seguir.  
  
```vb  
Dim custRow As DataRow = custTable.Rows(0)  
Dim custID As String = custRow("CustomerID", DataRowVersion.Original).ToString()  
```  
  
```csharp  
DataRow custRow = custTable.Rows[0];  
string custID = custRow["CustomerID", DataRowVersion.Original].ToString();  
```  
  
 A tabela a seguir dá a você uma breve descrição de cada valor de enumeração `DataRowVersion`.  
  
|Valor de DataRowVersion|Descrição|  
|--------------------------|-----------------|  
|<xref:System.Data.DataRowVersion.Current>|Os valores atuais para a linha. Esta versão de linha não existe para linhas com um `RowState` de `Deleted`.|  
|<xref:System.Data.DataRowVersion.Default>|A versão de linha padrão para uma linha específica. A versão de linha padrão para uma linha `Added`, `Modified` ou `Deleted` é `Current`. A versão de linha padrão para uma linha `Detached` é `Proposed`.|  
|<xref:System.Data.DataRowVersion.Original>|Os valores originais para a linha. Esta versão de linha não existe para linhas com um `RowState` de `Added`.|  
|<xref:System.Data.DataRowVersion.Proposed>|Os valores propostos para a linha. Esta versão de linha existe durante uma operação de edição em uma linha ou para uma linha que não faz parte de um `DataRowCollection`.|  
  
 Você pode testar se um `DataRow` tem uma versão de linha específica chamando o método <xref:System.Data.DataRow.HasVersion%2A> e passando `DataRowVersion` como argumento. Por exemplo, `DataRow.HasVersion(DataRowVersion.Original)` retornará `false` para linhas recém-adicionadas antes que `AcceptChanges` tenha sido chamado.  
  
 O exemplo de código a seguir exibe os valores em todas as linhas excluídas de uma tabela. As linhas `Deleted` não têm uma versão de linha `Current`; portanto, você deve passar `DataRowVersion.Original` ao acessar os valores de coluna.  
  
```vb  
Dim catTable As DataTable = catDS.Tables("Categories")  
  
Dim delRows() As DataRow = catTable.Select(Nothing, Nothing, DataViewRowState.Deleted)  
  
Console.WriteLine("Deleted rows:" & vbCrLf)  
  
Dim catCol As DataColumn  
Dim delRow As DataRow  
  
For Each catCol In catTable.Columns  
  Console.Write(catCol.ColumnName & vbTab)  
Next  
Console.WriteLine()  
  
For Each delRow In delRows  
  For Each catCol In catTable.Columns  
    Console.Write(delRow(catCol, DataRowVersion.Original) & vbTab)  
  Next  
  Console.WriteLine()  
Next  
```  
  
```csharp  
DataTable catTable = catDS.Tables["Categories"];  
  
DataRow[] delRows = catTable.Select(null, null, DataViewRowState.Deleted);  
  
Console.WriteLine("Deleted rows:\n");  
  
foreach (DataColumn catCol in catTable.Columns)  
  Console.Write(catCol.ColumnName + "\t");  
Console.WriteLine();  
  
foreach (DataRow delRow in delRows)  
{  
  foreach (DataColumn catCol in catTable.Columns)  
    Console.Write(delRow[catCol, DataRowVersion.Original] + "\t");  
  Console.WriteLine();  
}  
```  
  
## <a name="see-also"></a>Consulte também

- [Manipulando dados em uma DataTable](manipulating-data-in-a-datatable.md)
- [DataSets, DataTables e DataViews](index.md)
- [DataAdapters e DataReaders](../dataadapters-and-datareaders.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
