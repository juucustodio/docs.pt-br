---
description: 'Saiba mais sobre: Manipulando eventos DataAdapter'
title: Manipulação de eventos DataAdapter
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
ms.openlocfilehash: 045a48ae545ad4354844dd451ff58618b760a9a8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723940"
---
# <a name="handling-dataadapter-events"></a>Manipulação de eventos DataAdapter

O ADO.NET <xref:System.Data.Common.DataAdapter> expõe três eventos que você pode usar para responder a alterações feitas nos dados na fonte de dados. A tabela a seguir mostra os `DataAdapter` eventos.  
  
|Evento|Descrição|  
|-----------|-----------------|  
|`RowUpdating`|Uma operação UPDATE, INSER ou DELETE em uma linha (por meio da chamada a um dos métodos `Update`) está prestes a começar.|  
|`RowUpdated`|Uma operação UPDATE, INSER ou DELETE em uma linha (por meio da chamada a um dos métodos `Update`) está concluída.|  
|`FillError`|Ocorreu um erro durante uma operação `Fill`.|  
  
## <a name="rowupdating-and-rowupdated"></a>Auto-atualização e atualizado  

 `RowUpdating` é gerado antes que qualquer atualização em uma linha de <xref:System.Data.DataSet> tenha sido processada na fonte de dados. `RowUpdated` é gerado depois que qualquer atualização em uma linha de `DataSet` tenha sido processada na fonte de dados. Como resultado, você pode usar `RowUpdating` para modificar o comportamento da atualização antes que ela ocorra, para fornecer tratamento adicional quando ocorre uma atualização, para manter uma referência a uma linha atualizada, para cancelar a atualização atual e agendá-la para que um processo em lote seja processado posteriormente e assim por diante. `RowUpdated` é útil para responder a erros e exceções que ocorrem durante a atualização. Você pode adicionar informações de erro ao `DataSet` , bem como à lógica de repetição, e assim por diante.  
  
 Os argumentos <xref:System.Data.Common.RowUpdatingEventArgs> e <xref:System.Data.Common.RowUpdatedEventArgs> passados para os eventos `RowUpdating` e `RowUpdated` incluem o seguinte: uma propriedade `Command` que faz referência ao objeto `Command` que está sendo usado para executar a atualização; uma propriedade `Row` que faz referência ao objeto `DataRow` que contém as informações atualizadas; uma propriedade `StatementType` para qual tipo de atualização está sendo executada; a `TableMapping`, se aplicável; e a `Status` da operação.  
  
 Você pode usar a propriedade `Status` para determinar se ocorreu um erro durante a operação e, se desejar, para controlar as ações sobre as linhas atuais e resultantes. Quando o evento ocorre, a propriedade `Status` é igual a `Continue` ou `ErrorsOccurred`. A tabela a seguir mostra os valores para os quais você pode definir a propriedade `Status` para controlar as ações posteriores durante a atualização.  
  
|Status|Descrição|  
|------------|-----------------|  
|`Continue`|Continue com a operação de atualização.|  
|`ErrorsOccurred`|Anule a operação de atualização e lance uma exceção.|  
|`SkipCurrentRow`|Ignore a linha atual e continue com a operação de atualização.|  
|`SkipAllRemainingRows`|Anule a operação de atualização, mas não lance uma exceção.|  
  
 Definir a propriedade `Status` como `ErrorsOccurred` faz com que uma exceção seja lançada. Você pode controlar qual exceção é lançada definindo a propriedade `Errors` como a exceção desejada. O uso de um dos outros valores para `Status` impede que uma exceção seja gerada.  
  
 Você também pode usar a propriedade `ContinueUpdateOnError` para gerenciar os erros das linhas atualizadas. Se `DataAdapter.ContinueUpdateOnError` for `true`, quando a atualização de uma linha resultar no lançamento de uma exceção, o texto da exceção será colocado nas informações de `RowError` da linha específica e o processamento continuará sem lançar uma exceção. Isso permite que você responda aos erros quando a `Update` for concluída, ao contrário do evento `RowUpdated`, que lhe permite responder aos erros no momento em que eles são encontrados.  
  
 O exemplo de código a seguir mostra como adicionar e remover manipuladores de eventos. O manipulador de eventos `RowUpdating` grava um log com todos os registros excluídos com um carimbo de data/hora. O manipulador de eventos `RowUpdated` adiciona informações de erro à propriedade `RowError` da linha em `DataSet`, suprime a exceção e continua o processamento (espelhando o comportamento de `ContinueUpdateOnError` = `true`).  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
  
' Add handlers.  
AddHandler custAdapter.RowUpdating, New SqlRowUpdatingEventHandler( _  
  AddressOf OnRowUpdating)  
AddHandler custAdapter.RowUpdated, New SqlRowUpdatedEventHandler(  
  AddressOf OnRowUpdated)  
  
' Set DataAdapter command properties, fill DataSet, and modify DataSet.  
  
custAdapter.Update(custDS, "Customers")  
  
' Remove handlers.  
RemoveHandler custAdapter.RowUpdating, _  
  New SqlRowUpdatingEventHandler(AddressOf OnRowUpdating)  
RemoveHandler custAdapter.RowUpdated, _  
  New SqlRowUpdatedEventHandler(AddressOf OnRowUpdated)  
  
Private Shared Sub OnRowUpdating(sender As Object, _  
  args As SqlRowUpdatingEventArgs)  
  If args.StatementType = StatementType.Delete Then  
    Dim tw As System.IO.TextWriter = _  
  System.IO.File.AppendText("Deletes.log")  
    tw.WriteLine( _  
      "{0}: Customer {1} Deleted.", DateTime.Now, args.Row(_  
      "CustomerID", DataRowVersion.Original))  
    tw.Close()  
  End If  
End Sub  
  
Private Shared Sub OnRowUpdated( _  
  sender As Object, args As SqlRowUpdatedEventArgs)  
  If args.Status = UpdateStatus.ErrorsOccurred  
    args.Status = UpdateStatus.SkipCurrentRow  
    args.Row.RowError = args.Errors.Message  
  End If  
End Sub  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
  
// Add handlers.  
custAdapter.RowUpdating += new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated += new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
// Set DataAdapter command properties, fill DataSet, modify DataSet.  
  
custAdapter.Update(custDS, "Customers");  
  
// Remove handlers.  
custAdapter.RowUpdating -= new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated -= new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
protected static void OnRowUpdating(  
  object sender, SqlRowUpdatingEventArgs args)  
{  
  if (args.StatementType == StatementType.Delete)  
  {  
    System.IO.TextWriter tw = System.IO.File.AppendText("Deletes.log");  
    tw.WriteLine(  
      "{0}: Customer {1} Deleted.", DateTime.Now,
       args.Row["CustomerID", DataRowVersion.Original]);  
    tw.Close();  
  }  
}  
  
protected static void OnRowUpdated(  
  object sender, SqlRowUpdatedEventArgs args)  
{  
  if (args.Status == UpdateStatus.ErrorsOccurred)  
  {  
    args.Row.RowError = args.Errors.Message;  
    args.Status = UpdateStatus.SkipCurrentRow;  
  }  
}  
```  
  
## <a name="fillerror"></a>FillError  

 `DataAdapter` emite o evento `FillError` quando ocorre um erro durante uma operação `Fill`. Esse tipo de erro geralmente ocorre quando os dados na linha que está sendo adicionada não podem ser convertidos em um tipo de .NET Framework sem perda de precisão.  
  
 Se ocorrer um erro durante uma operação `Fill`, a linha atual não será adicionada à `DataTable`. O evento `FillError` permite que você resolva o erro e adicione a linha ou ignore a linha excluída e continue com a operação `Fill`.  
  
 O `FillErrorEventArgs` passado para o evento `FillError` pode conter várias propriedades que lhe permitem responder aos erros e resolvê-los. A tabela a seguir mostra as propriedades do objeto `FillErrorEventArgs`.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`Errors`|O `Exception` que ocorreu.|  
|`DataTable`|O objeto `DataTable` que estava sendo preenchido quando o erro ocorreu.|  
|`Values`|A matriz de objetos que contém os valores da linha que estava sendo adicionada quando o erro ocorreu. As referências ordinais da matriz `Values` correspondem às referências ordinais das colunas da linha que está sendo adicionada. Por exemplo, `Values[0]` é o valor que estava sendo adicionado como a primeira coluna da linha.|  
|`Continue`|Permite que você escolha se deseja ou não lançar uma exceção. Definir a propriedade `Continue` como `false` interromperá a operação `Fill` atual e lançará uma exceção. A configuração de `Continue` como `true` permite continuar com a operação `Fill` apesar do erro.|  
  
 O exemplo de código a seguir adiciona um manipulador de eventos para o evento `FillError` de `DataAdapter`. No código do evento `FillError`, o exemplo determina se há o potencial para perda de precisão, fornecendo a oportunidade de responder à exceção.  
  
```vb  
AddHandler adapter.FillError, New FillErrorEventHandler( _  
  AddressOf FillError)  
  
Dim dataSet As DataSet = New DataSet  
adapter.Fill(dataSet, "ThisTable")  
  
Private Shared Sub FillError(sender As Object, _  
  args As FillErrorEventArgs)  
  If args.Errors.GetType() Is Type.GetType("System.OverflowException") Then  
    ' Code to handle precision loss.  
    ' Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(New Object() _  
      {args.Values(0), args.Values(1), DBNull.Value})  
    ' Set the RowError containing the value for the third column.  
    myRow.RowError = _  
      "OverflowException encountered. Value from data source: " & _  
      args.Values(2)  
    args.Continue = True  
  End If  
End Sub  
```  
  
```csharp  
adapter.FillError += new FillErrorEventHandler(FillError);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "ThisTable");  
  
protected static void FillError(object sender, FillErrorEventArgs args)  
{  
  if (args.Errors.GetType() == typeof(System.OverflowException))  
  {  
    // Code to handle precision loss.  
    //Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(new object[]  
       {args.Values[0], args.Values[1], DBNull.Value});  
    //Set the RowError containing the value for the third column.  
    myRow.RowError =
       "OverflowException Encountered. Value from data source: " +  
       args.Values[2];  
    args.Continue = true;  
  }  
}  
```  
  
## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [Manipular eventos do DataSet](./dataset-datatable-dataview/handling-dataset-events.md)
- [Manipulação de eventos de DataTable](./dataset-datatable-dataview/handling-datatable-events.md)
- [Eventos](../../../standard/events/index.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
