---
description: 'Saiba mais sobre: execução de operações em lote usando adaptadores de'
title: Executando operações em lote usando DataAdapters
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
ms.openlocfilehash: d0472761a0a3893872f073cfe25921066a0f96bd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672329"
---
# <a name="performing-batch-operations-using-dataadapters"></a>Executando operações em lote usando DataAdapters

O suporte a lotes no ADO.NET permite que um <xref:System.Data.Common.DataAdapter> agrupe operações INSERT, UPDATE e DELETE de um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> para o servidor, em vez de enviar uma operação de cada vez. A redução no número de viagens de ida e volta para o servidor costuma resultar em ganhos significativos de desempenho. Atualizações em lotes têm suporte nos provedores de dados .NET para SQL Server (<xref:System.Data.SqlClient>) e Oracle (<xref:System.Data.OracleClient>).  
  
 Ao atualizar um banco de dados com alterações de um <xref:System.Data.DataSet> em versões anteriores do ADO.NET, o método `Update` de um `DataAdapter` executava atualizações no banco de dados em uma linha por vez. Ao iterar pelas linhas no <xref:System.Data.DataTable> especificado, ele revisava cada <xref:System.Data.DataRow> para verificar se ocorreram modificações. Se a linha tivesse sido alterada, ele chamava o `UpdateCommand`, `InsertCommand` ou `DeleteCommand` apropriado, dependendo do valor da propriedade <xref:System.Data.DataRow.RowState%2A> para essa linha. Cada atualização de linha envolvia uma viagem de ida e volta da rede ao banco de dados.  
  
 A partir do ADO.NET 2.0, o <xref:System.Data.Common.DbDataAdapter> expõe uma propriedade <xref:System.Data.Common.DbDataAdapter.UpdateBatchSize%2A>. Definir o `UpdateBatchSize` com um valor inteiro positivo causa o envio de atualizações do banco de dados como lotes de tamanho especificado. Por exemplo, a definição do `UpdateBatchSize` como 10 agrupará 10 instruções separadas e as submeterá como um único lote. Definir o `UpdateBatchSize` como 0 fará com que o <xref:System.Data.Common.DataAdapter> use o maior tamanho de lotes que o servidor possa manipular. Defini-lo como 1 desabilitará atualizações em lotes, pois as linhas são enviadas uma de cada vez.  
  
 Executar um lote extremamente grande pode diminuir o desempenho. Portanto, você deve testar para verificar qual é a melhor configuração de tamanho de lote antes de implementar seu aplicativo.  
  
## <a name="using-the-updatebatchsize-property"></a>Usando a propriedade UpdateBatchSize  

 Quando atualizações em lotes são habilitadas, o valor da propriedade <xref:System.Data.IDbCommand.UpdatedRowSource%2A> de `UpdateCommand`, de `InsertCommand` e de `DeleteCommand` do DataAdapter deve ser definido como <xref:System.Data.UpdateRowSource.None> ou <xref:System.Data.UpdateRowSource.OutputParameters>. Ao executar uma atualização em lotes, o valor da propriedade <xref:System.Data.IDbCommand.UpdatedRowSource%2A> do comando de <xref:System.Data.UpdateRowSource.FirstReturnedRecord> ou de <xref:System.Data.UpdateRowSource.Both> é inválido.  
  
 O procedimento a seguir demonstra o uso da propriedade `UpdateBatchSize`. O procedimento tem dois argumentos, um objeto <xref:System.Data.DataSet> com colunas que representam os campos **ProductCategoryID** e **Name** na tabela **Production.ProductCategory** e um inteiro que representa o tamanho do lote (o número de linhas no lote). O código cria um novo objeto <xref:System.Data.SqlClient.SqlDataAdapter>, definindo suas propriedades <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> e <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A>. O código pressupõe que o objeto <xref:System.Data.DataSet> alterou linhas. Ele define a propriedade `UpdateBatchSize` e executa a atualização.  
  
```vb  
Public Sub BatchUpdate( _  
  ByVal dataTable As DataTable, ByVal batchSize As Int32)  
    ' Assumes GetConnectionString() returns a valid connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    ' Connect to the AdventureWorks database.  
    Using connection As New SqlConnection(connectionString)  
        ' Create a SqlDataAdapter.  
        Dim adapter As New SqlDataAdapter()  
  
        'Set the UPDATE command and parameters.  
        adapter.UpdateCommand = New SqlCommand( _  
          "UPDATE Production.ProductCategory SET " _  
          & "Name=@Name WHERE ProductCategoryID=@ProdCatID;", _  
          connection)  
        adapter.UpdateCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",  _  
          SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.UpdateCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the INSERT command and parameter.  
        adapter.InsertCommand = New SqlCommand( _  
          "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);", _  
  connection)  
        adapter.InsertCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.InsertCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the DELETE command and parameter.  
        adapter.DeleteCommand = New SqlCommand( _  
          "DELETE FROM Production.ProductCategory " _  
          & "WHERE ProductCategoryID=@ProdCatID;", connection)  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID", _  
           SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None  
  
        ' Set the batch size.  
        adapter.UpdateBatchSize = batchSize  
  
        ' Execute the update.  
        adapter.Update(dataTable)  
    End Using  
End Sub  
```  
  
```csharp  
public static void BatchUpdate(DataTable dataTable,Int32 batchSize)  
{  
    // Assumes GetConnectionString() returns a valid connection string.  
    string connectionString = GetConnectionString();  
  
    // Connect to the AdventureWorks database.  
    using (SqlConnection connection = new
      SqlConnection(connectionString))  
    {  
  
        // Create a SqlDataAdapter.  
        SqlDataAdapter adapter = new SqlDataAdapter();  
  
        // Set the UPDATE command and parameters.  
        adapter.UpdateCommand = new SqlCommand(  
            "UPDATE Production.ProductCategory SET "  
            + "Name=@Name WHERE ProductCategoryID=@ProdCatID;",
            connection);  
        adapter.UpdateCommand.Parameters.Add("@Name",
           SqlDbType.NVarChar, 50, "Name");  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",
           SqlDbType.Int, 4, "ProductCategoryID");  
         adapter.UpdateCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the INSERT command and parameter.  
        adapter.InsertCommand = new SqlCommand(  
            "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);",
            connection);  
        adapter.InsertCommand.Parameters.Add("@Name",
          SqlDbType.NVarChar, 50, "Name");  
        adapter.InsertCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the DELETE command and parameter.  
        adapter.DeleteCommand = new SqlCommand(  
            "DELETE FROM Production.ProductCategory "  
            + "WHERE ProductCategoryID=@ProdCatID;", connection);  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID",
          SqlDbType.Int, 4, "ProductCategoryID");  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the batch size.  
        adapter.UpdateBatchSize = batchSize;  
  
        // Execute the update.  
        adapter.Update(dataTable);  
    }  
}  
```  
  
## <a name="handling-batch-update-related-events-and-errors"></a>Manipulando eventos relativos à atualização em lotes e erros  

 O **DataAdapter** tem dois eventos relacionados à atualização: **RowUpdating** e **RowUpdated**. Em versões anteriores do ADO.NET, quando o processamento em lotes estava desabilitado, cada um desses eventos era gerado uma vez para cada linha processada. A **auto-atualização é gerada** antes que a atualização ocorra, e o **auto-atualização** é gerado após a conclusão da atualização do banco de dados.  
  
### <a name="event-behavior-changes-with-batch-updates"></a>Alterações de comportamento dos eventos com atualizações em lotes  

 Quando o processamento em lotes está habilitado, várias linhas são atualizadas em uma única operação de banco de dados. Portanto, somente um evento `RowUpdated` ocorre para cada lote, enquanto o evento `RowUpdating` ocorre para cada linha processada. Quando o processamento em lotes está desabilitado, os dois eventos são disparados com interpolação um a um, onde um evento `RowUpdating` e um evento `RowUpdated` são disparados para uma linha e, depois, um evento `RowUpdating` e um evento `RowUpdated` são disparados para a próxima linha, até que todas as linhas sejam processadas.  
  
### <a name="accessing-updated-rows"></a>Acessando linhas atualizadas  

 Quando o processamento em lotes está desabilitado, a linha que está sendo atualizada pode ser acessada usando a propriedade <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A> da classe <xref:System.Data.Common.RowUpdatedEventArgs>.  
  
 Quando o processamento em lotes está habilitado, um único evento `RowUpdated` é gerado para várias linhas. Portanto, o valor da propriedade `Row` para cada linha é nulo. Os eventos `RowUpdating` ainda são gerados para cada linha. O método <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> da classe <xref:System.Data.Common.RowUpdatedEventArgs> permite que você acesse as linhas processadas copiando referências às linhas em uma matriz. Se nenhuma linha está sendo processada, `CopyToRows` gera <xref:System.ArgumentNullException>. Use a propriedade <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A> para retornar o número de linhas processadas antes de chamar o método <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A>.  
  
### <a name="handling-data-errors"></a>Manipulando erros de dados  

 A execução em lotes tem o mesmo efeito que a execução de cada instrução individual. As instruções são executadas na ordem em que elas foram adicionados ao lote. O tratamento de erros no modo em lotes é o mesmo de quando esse modo está desabilitado. Cada linha é processada separadamente. Somente linhas que foram processadas com êxito no banco de dados serão atualizadas na <xref:System.Data.DataRow> correspondente dentro da <xref:System.Data.DataTable>.  
  
 O provedor de dados e o servidor de banco de dados back-end determinam que construções SQL têm suporte para a execução em lotes. Uma exceção pode ser gerada quando uma instrução sem suporte é enviada para execução.  
  
## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [Atualizando fontes de dados com DataAdapters](updating-data-sources-with-dataadapters.md)
- [Manipulação de eventos DataAdapter](handling-dataadapter-events.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
