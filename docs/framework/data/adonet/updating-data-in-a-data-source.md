---
description: 'Saiba mais sobre: Atualizando dados em uma fonte de dados'
title: Atualizando dados em uma fonte de dados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 55c545e5-dcd5-4323-a5b9-3825c2157462
ms.openlocfilehash: a55d6a53f4607908fa279474419803eac3963909
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766563"
---
# <a name="updating-data-in-a-data-source"></a>Atualizando dados em uma fonte de dados

As instruções SQL que modificam dados (como UPDATE, INSERT ou DELETE) não retornam linhas. Da mesma forma, muitos procedimentos armazenados executam uma ação, mas não retornam linhas. Para executar comandos que não retornam linhas, crie um objeto **Command** com o comando SQL apropriado e um **Connection**, incluindo os **Parâmetros** necessários. Execute o comando com o método **ExecuteNonQuery** do objeto **Command** .  
  
 O método **ExecuteNonQuery** retorna um número inteiro que representa o número de linhas afetadas pela instrução ou pelo procedimento armazenado que foi executado. Se várias instruções tiverem sido executadas, o valor retornado é a soma dos registros afetados por todas as instruções executadas.  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir executa uma instrução INSERT para inserir um registro em um banco de dados usando **ExecuteNonQuery**.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
connection.Open()  
  
Dim queryString As String = "INSERT INTO Customers " & _  
  "(CustomerID, CompanyName) Values('NWIND', 'Northwind Traders')"  
  
Dim command As SqlCommand = New SqlCommand(queryString, connection)  
Dim recordsAffected As Int32 = command.ExecuteNonQuery()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
connection.Open();  
  
string queryString = "INSERT INTO Customers " +  
  "(CustomerID, CompanyName) Values('NWIND', 'Northwind Traders')";  
  
SqlCommand command = new SqlCommand(queryString, connection);  
Int32 recordsAffected = command.ExecuteNonQuery();  
```  
  
 O exemplo de código a seguir executa o procedimento armazenado criado pelo exemplo de código em [Executar operações de catálogo](performing-catalog-operations.md). Nenhuma linha é retornada pelo procedimento armazenado, portanto, o método **ExecuteNonQuery** é usado, mas o procedimento armazenado recebe um parâmetro de entrada e retorna um parâmetro de saída e um valor.  
  
 Para o <xref:System.Data.OleDb.OleDbCommand> objeto, o parâmetro **ReturnValue** deve ser adicionado primeiro à coleção **Parameters** .  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim command As SqlCommand = _  
   New SqlCommand("InsertCategory" , connection)  
command.CommandType = CommandType.StoredProcedure  
  
Dim parameter As SqlParameter = _  
 command.Parameters.Add("@RowCount", SqlDbType.Int)  
parameter.Direction = ParameterDirection.ReturnValue  
  
parameter = command.Parameters.Add( _  
  "@CategoryName", SqlDbType.NChar, 15)  
  
parameter = command.Parameters.Add("@Identity", SqlDbType.Int)  
parameter.Direction = ParameterDirection.Output  
  
command.Parameters("@CategoryName").Value = "New Category"  
command.ExecuteNonQuery()  
  
Dim categoryID As Int32 = CInt(command.Parameters("@Identity").Value)  
Dim rowCount As Int32 = CInt(command.Parameters("@RowCount").Value)
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
SqlCommand command = new SqlCommand("InsertCategory" , connection);  
command.CommandType = CommandType.StoredProcedure;  
  
SqlParameter parameter = command.Parameters.Add(  
  "@RowCount", SqlDbType.Int);  
parameter.Direction = ParameterDirection.ReturnValue;  
  
parameter = command.Parameters.Add(  
  "@CategoryName", SqlDbType.NChar, 15);  
  
parameter = command.Parameters.Add("@Identity", SqlDbType.Int);  
parameter.Direction = ParameterDirection.Output;  
  
command.Parameters["@CategoryName"].Value = "New Category";  
command.ExecuteNonQuery();  
  
Int32 categoryID = (Int32) command.Parameters["@Identity"].Value;  
Int32 rowCount = (Int32) command.Parameters["@RowCount"].Value;  
```  
  
## <a name="see-also"></a>Consulte também

- [Usando comandos para modificar dados](using-commands-to-modify-data.md)
- [Atualizando fontes de dados com DataAdapters](updating-data-sources-with-dataadapters.md)
- [Comandos e parâmetros](commands-and-parameters.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
