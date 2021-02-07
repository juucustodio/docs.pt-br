---
description: 'Saiba mais sobre: edições de DataTable'
title: Edições de DataTable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f08008a9-042e-4de9-94f3-4f0e502b1eb5
ms.openlocfilehash: 983a4016fbdb71baa3bcd4ce8a34175d10b604d2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739463"
---
# <a name="datatable-edits"></a>Edições de DataTable

Quando você altera os valores de coluna em uma <xref:System.Data.DataRow>, as alterações são colocadas imediatamente no estado atual da linha. O <xref:System.Data.DataRowState> é então definido como **Modified**, e as alterações são aceitas ou rejeitadas usando os <xref:System.Data.DataRow.AcceptChanges%2A> <xref:System.Data.DataRow.RejectChanges%2A> métodos ou da **DataRow**. A **DataRow** também fornece três métodos que você pode usar para suspender o estado da linha enquanto estiver editando. Esses métodos são <xref:System.Data.DataRow.BeginEdit%2A>, <xref:System.Data.DataRow.EndEdit%2A> e <xref:System.Data.DataRow.CancelEdit%2A>.  
  
 Quando você modifica valores de coluna em uma **DataRow** diretamente, o **DataRow** gerencia os valores de coluna usando as versões de linha **atual**, **padrão** e **original** . Além dessas versões de linha, os métodos **BeginEdit**, **EndEdit** e **CancelEdit** usam uma quarta versão de linha: **proposta**. Para obter mais informações sobre versões de linha, consulte [Estados de linha e versões de linha](row-states-and-row-versions.md).  
  
 A versão de linha **proposta** existe durante uma operação de edição que começa chamando **BeginEdit** e que termina usando **EndEdit** ou **CancelEdit,** ou chamando **AcceptChanges** ou **RejectChanges**.  
  
 Durante a operação de edição, você pode aplicar a lógica de validação a colunas individuais avaliando o **ProposedValue** no evento **ColumnChanged** da **DataTable**. O evento **ColumnChanged** contém **DataColumnChangeEventArgs** que mantêm uma referência à coluna que está sendo alterada e ao **ProposedValue**. Depois que você avaliar o valor proposto, poderá modificá-lo ou cancelar a edição. Quando a edição é finalizada, a linha sai do estado **proposto** .  
  
 Você pode confirmar as edições chamando **EndEdit** ou pode cancelá-las chamando **CancelEdit**. Observe que, embora **EndEdit** confirme suas edições, o **conjunto de DataSet** não aceita realmente as alterações até que **AcceptChanges** seja chamado. Observe também que, se você chamar **AcceptChanges** antes de terminar a edição com **EndEdit** ou **CancelEdit**, a edição será finalizada e os valores de linha **proposto** serão aceitos para as versões de linha **atuais** e **originais** . Da mesma maneira, chamar **RejectChanges** encerra a edição e descarta as versões de linha **atuais** e **propostas** . Chamar **EndEdit** ou **CancelEdit** depois de chamar **AcceptChanges** ou **RejectChanges** não tem efeito porque a edição já terminou.  
  
 O exemplo a seguir demonstra como usar **BeginEdit** com **EndEdit** e **CancelEdit**. O exemplo também verifica o **ProposedValue** no evento **ColumnChanged** e decide se a edição deve ser cancelada.  
  
```vb  
Dim workTable As DataTable = New DataTable  
workTable.Columns.Add("LastName", Type.GetType("System.String"))  
  
AddHandler workTable.ColumnChanged, _  
  New DataColumnChangeEventHandler(AddressOf OnColumnChanged)  
  
Dim workRow As DataRow = workTable.NewRow()  
workRow(0) = "Smith"  
workTable.Rows.Add(workRow)  
  
workRow.BeginEdit()  
' Causes the ColumnChanged event to write a message and cancel the edit.  
workRow(0) = ""
workRow.EndEdit()  
  
' Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow(0), workRow.RowState)  
  
Private Shared Sub OnColumnChanged( _  
  sender As Object, args As DataColumnChangeEventArgs)  
  If args.Column.ColumnName = "LastName" Then  
    If args.ProposedValue.ToString() = "" Then  
      Console.WriteLine("Last Name cannot be blank.  Edit canceled.")  
      args.Row.CancelEdit()  
    End If  
  End If  
End Sub  
```  
  
```csharp  
DataTable workTable  = new DataTable();  
workTable.Columns.Add("LastName", typeof(String));  
  
workTable.ColumnChanged +=
  new DataColumnChangeEventHandler(OnColumnChanged);  
  
DataRow workRow = workTable.NewRow();  
workRow[0] = "Smith";  
workTable.Rows.Add(workRow);  
  
workRow.BeginEdit();  
// Causes the ColumnChanged event to write a message and cancel the edit.  
workRow[0] = "";
workRow.EndEdit();  
  
// Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow[0], workRow.RowState);
  
protected static void OnColumnChanged(  
  Object sender, DataColumnChangeEventArgs args)  
{  
  if (args.Column.ColumnName == "LastName")  
    if (args.ProposedValue.ToString() == "")  
    {  
      Console.WriteLine("Last Name cannot be blank. Edit canceled.");  
      args.Row.CancelEdit();  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataRow>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataRowVersion>
- [Manipulando dados em uma DataTable](manipulating-data-in-a-datatable.md)
- [Manipulação de eventos de DataTable](handling-datatable-events.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
