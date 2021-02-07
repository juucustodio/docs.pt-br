---
description: 'Saiba mais sobre: GetSchema e coleções de esquema'
title: GetSchema e coleções de esquema
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7ab93b89-1221-427c-84ad-04803b3c64b4
ms.openlocfilehash: 2b085435f0f9ea9ec33897ee417cd7a726c4503d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723979"
---
# <a name="getschema-and-schema-collections"></a>GetSchema e coleções de esquema

As classes de **conexão** em cada um dos provedores gerenciados .NET Framework implementam um método **GetSchema** que é usado para recuperar informações de esquema sobre o banco de dados que está conectado no momento e as informações de esquema retornadas do método **GetSchema** vêm na forma de um <xref:System.Data.DataTable> . O método **GetSchema** é um método sobrecarregado que fornece parâmetros opcionais para especificar a coleção de esquemas a ser retornada e restringir a quantidade de informações retornada.  
  
## <a name="specifying-the-schema-collections"></a>Especificando as coleções de esquema  

 O primeiro parâmetro opcional do método **GetSchema** é o nome da coleção que é especificado como uma cadeia de caracteres. Há dois tipos de coleções de esquemas: as coleções de esquemas que são comuns a todos os provedores e as coleções de esquemas específicas de cada provedor.  
  
 Você pode consultar um provedor gerenciado .NET Framework para determinar a lista de coleções de esquema com suporte chamando o método **GetSchema** sem argumentos ou com o nome da coleção de esquema "MetaDataCollections". Isso retornará uma <xref:System.Data.DataTable> com uma lista de coleções de esquemas compatíveis, o número de restrições ao qual cada uma dá suporte e o número de partes de identificador usado por elas.  
  
### <a name="retrieving-schema-collections-example"></a>Exemplo de recuperação de coleções de esquema  

 Os exemplos a seguir demonstram como usar o <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> método do .NET Framework provedor de dados para a <xref:System.Data.SqlClient.SqlConnection> classe SQL Server para recuperar informações de esquema sobre todas as tabelas contidas no banco de dados de exemplo **AdventureWorks** :  
  
```vb  
Imports System.Data.SqlClient  
  
Module Module1  
   Sub Main()  
      Dim connectionString As String = GetConnectionString()  
      Using connection As New SqlConnection(connectionString)  
         'Connect to the database then retrieve the schema information.  
         connection.Open()  
         Dim table As DataTable = connection.GetSchema("Tables")  
  
         ' Display the contents of the table.  
         DisplayData(table)  
         Console.WriteLine("Press any key to continue.")  
         Console.ReadKey()  
      End Using  
   End Sub  
  
   Private Function GetConnectionString() As String  
      ' To avoid storing the connection string in your code,
      ' you can retrieve it from a configuration file.  
      Return "Data Source=(local);Database=AdventureWorks;" _  
         & "Integrated Security=true;"  
   End Function  
  
   Private Sub DisplayData(ByVal table As DataTable)  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
   End Sub  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Program  
{  
  static void Main()  
  {  
  string connectionString = GetConnectionString();  
  using (SqlConnection connection = new SqlConnection(connectionString))  
  {  
   // Connect to the database then retrieve the schema information.  
   connection.Open();  
   DataTable table = connection.GetSchema("Tables");  
  
   // Display the contents of the table.  
   DisplayData(table);  
   Console.WriteLine("Press any key to continue.");  
   Console.ReadKey();  
   }  
 }  
  
  private static string GetConnectionString()  
  {  
   // To avoid storing the connection string in your code,  
   // you can retrieve it from a configuration file.  
   return "Data Source=(local);Database=AdventureWorks;" +  
      "Integrated Security=true;";  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
     foreach (System.Data.DataRow row in table.Rows)  
     {  
        foreach (System.Data.DataColumn col in table.Columns)  
        {  
           Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
        }  
     Console.WriteLine("============================");  
     }  
  }  
}  
```  
  
## <a name="see-also"></a>Confira também

- [Como recuperar informações de esquema de banco de dados](retrieving-database-schema-information.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
