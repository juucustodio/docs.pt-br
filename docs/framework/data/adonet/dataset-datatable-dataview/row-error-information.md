---
description: 'Saiba mais sobre: informações de erro de linha'
title: Informações de erro de linha
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8b1f9070-d032-48c7-b030-bd8fbb2ca59a
ms.openlocfilehash: d3eb8b20893ad47720ebb03ad4ab61940f014bd3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651685"
---
# <a name="row-error-information"></a>Informações de erro de linha

Para evitar a resposta a erros de linha durante a edição de valores em um <xref:System.Data.DataTable> , você pode adicionar as informações de erro à linha para uso posterior. O <xref:System.Data.DataRow> objeto fornece uma <xref:System.Data.DataRow.RowError%2A> propriedade em cada linha para essa finalidade. A adição de dados à propriedade **Usererror** de uma **DataRow** define a <xref:System.Data.DataRow.HasErrors%2A> propriedade da **DataRow** como **true**. Se a **DataRow** for parte de uma **DataTable** e **DataRow. HasErrors** for **true**, a propriedade **DataTable. HasErrors** também será **verdadeira**. Isso se aplica também ao **conjunto de conjuntos** ao qual a **DataTable** pertence. Ao testar erros, você pode verificar a propriedade **HasErrors** para determinar se as informações de erro foram adicionadas a qualquer linha. Se o **HasErrors** for **true**, você poderá usar o <xref:System.Data.DataTable.GetErrors%2A> método da **DataTable** para retornar e examinar apenas as linhas com erros, conforme mostrado no exemplo a seguir.  
  
```vb  
Dim workTable As DataTable = New DataTable("Customers")  
workTable.Columns.Add("CustID", Type.GetType("System.Int32"))  
workTable.Columns.Add("Total", Type.GetType("System.Double"))  
  
AddHandler workTable.RowChanged, New DataRowChangeEventHandler(AddressOf OnRowChanged)  
  
Dim i  As Int32  
  
For i  = 0 To 10  
  workTable.Rows.Add(New Object() {i , i *100})  
Next  
  
If workTable.HasErrors Then  
  Console.WriteLine("Errors in Table " & workTable.TableName)  
  
  Dim myRow As DataRow  
  
  For Each myRow In workTable.GetErrors()  
    Console.WriteLine("CustID = " & myRow("CustID").ToString())  
    Console.WriteLine(" Error = " & myRow.RowError & vbCrLf)  
  Next  
End If  
  
Private Shared Sub OnRowChanged( _  
    sender As Object, args As DataRowChangeEventArgs)  
  ' Check for zero values.  
  If CDbl(args.Row("Total")) = 0 Then args.Row.RowError = _  
      "Total cannot be 0."  
End Sub  
```  
  
```csharp  
DataTable  workTable = new DataTable("Customers");  
workTable.Columns.Add("CustID", typeof(Int32));  
workTable.Columns.Add("Total", typeof(Double));  
  
workTable.RowChanged += new DataRowChangeEventHandler(OnRowChanged);  
  
for (int i = 0; i < 10; i++)  
  workTable.Rows.Add(new Object[] {i, i*100});  
  
if (workTable.HasErrors)  
{  
  Console.WriteLine("Errors in Table " + workTable.TableName);  
  
  foreach (DataRow myRow in workTable.GetErrors())  
  {  
    Console.WriteLine("CustID = " + myRow["CustID"]);  
    Console.WriteLine(" Error = " + myRow.RowError + "\n");  
  }  
}  
  
protected static void OnRowChanged(  
    Object sender, DataRowChangeEventArgs args)  
{  
  // Check for zero values.  
  if (args.Row["Total"].Equals(0D))  
    args.Row.RowError = "Total cannot be 0.";  
}  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataRow>
- <xref:System.Data.DataTable>
- [Manipulando dados em uma DataTable](manipulating-data-in-a-datatable.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
