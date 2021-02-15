---
description: 'Saiba mais sobre: sequências Oracle'
title: Sequências da Oracle
ms.date: 03/30/2017
ms.assetid: 27cd371d-8252-414d-b5b2-5d31fa44b585
ms.openlocfilehash: dea0a0ba0e39410a92b293186a5bd12477113d60
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672420"
---
# <a name="oracle-sequences"></a>Sequências da Oracle

O provedor de dados .NET Framework para Oracle fornece suporte para recuperar os principais valores do Oracle Sequence gerados pelo servidor depois de executar inserções usando o <xref:System.Data.OracleClient.OracleDataAdapter>.  
  
 O SQL Server e a Oracle dão suporte à criação de incrementar automaticamente as colunas que podem ser designadas como chaves primárias. Esses valores gerados pelo servidor como linhas são adicionados a uma tabela. No SQL Server, você define a propriedade Identity de uma coluna; no Oracle, você cria uma Sequence. A diferença entre colunas incrementar automaticamente colunas no SQL Server e sequências no Oracle é que:  
  
- No SQL Server, você marca uma coluna como uma coluna de incremento automático e o SQL Server automaticamente gera novos valores para a coluna quando você insere uma nova linha.  
  
- No Oracle, você cria uma sequência para gerar novos valores para uma coluna na tabela, mas não há nenhum link direto entre a sequência e a tabela ou coluna. Uma sequência do Oracle é um objeto, como uma tabela ou procedimento armazenado.  
  
 Quando você cria uma sequência em um banco de dados Oracle, pode definir seu valor inicial e o incremento entre seus valores. Você também pode consultar a sequência para novos valores antes de enviar novas linhas. Isso significa que seu código pode reconhecer os principais valores para novas linhas antes de inseri-los no banco de dados.  
  
 Para obter mais informações sobre como criar colunas de incremento automático usando SQL Server e ADO.NET, consulte [recuperando identidade ou valores autonumerados](retrieving-identity-or-autonumber-values.md) e [criando colunas AutoIncrement](./dataset-datatable-dataview/creating-autoincrement-columns.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo C# a seguir demonstra como você pode recuperar novos valores de sequência no banco de dados Oracle. O exemplo faz referência à sequência na consulta INSERT INTO usada para enviar as novas linhas e, em seguida, retorna o valor da sequência gerado usando a cláusula RETURNING introduzida no Oracle10g. O exemplo adiciona uma série de novas linhas pendentes em um <xref:System.Data.DataTable> usando a funcionalidade de incremento automático do ADO.NET para gerar valores de chave primária de “espaço reservado”. Observe que o valor de incremento gerado pelo ADO.NET para a nova linha é apenas um "espaço reservado". Isso significa que o banco de dados pode gerar valores diferentes dos que o ADO.NET produz.  
  
 Antes de enviar as inserções pendentes para o banco de dados, o exemplo exibe o conteúdo das linhas. Em seguida, o código cria um novo objeto <xref:System.Data.OracleClient.OracleDataAdapter> e define seu <xref:System.Data.OracleClient.OracleDataAdapter.InsertCommand%2A> e as propriedades <xref:System.Data.OracleClient.OracleDataAdapter.UpdateBatchSize%2A>. O exemplo também fornece a lógica para retornar os valores gerados pelo servidor usando os parâmetros de saída. Em seguida, o exemplo executa a atualização para enviar as linhas pendentes e exibe o conteúdo do <xref:System.Data.DataTable>.  
  
```csharp  
public void OracleSequence(String connectionString)  
{  
   String insertString =
      "INSERT INTO SequenceTest_Table (ID, OtherColumn)" +  
      "VALUES (SequenceTest_Sequence.NEXTVAL, :OtherColumn)" +  
      "RETURNING ID INTO :ID";  
  
   using (OracleConnection conn = new OracleConnection(connectionString))  
   {  
      //Open a connection.  
      conn.Open();  
      OracleCommand cmd = conn.CreateCommand();  
  
      // Prepare the database.  
      cmd.CommandText = "DROP SEQUENCE SequenceTest_Sequence";  
      try { cmd.ExecuteNonQuery(); } catch { }  
  
      cmd.CommandText = "DROP TABLE SequenceTest_Table";  
      try { cmd.ExecuteNonQuery(); } catch { }  
  
      cmd.CommandText = "CREATE TABLE SequenceTest_Table " +  
                     "(ID int PRIMARY KEY, OtherColumn varchar(255))";  
      cmd.ExecuteNonQuery();  
  
      cmd.CommandText = "CREATE SEQUENCE SequenceTest_Sequence " +  
                        "START WITH 100 INCREMENT BY 5";  
      cmd.ExecuteNonQuery();  
  
      DataTable testTable = new DataTable();  
      DataColumn column = testTable.Columns.Add("ID", typeof(int));  
      column.AutoIncrement = true;  
      column.AutoIncrementSeed = -1;  
      column.AutoIncrementStep = -1;  
      testTable.PrimaryKey = new DataColumn[] { column };  
      testTable.Columns.Add("OtherColumn", typeof(string));  
      for (int rowCounter = 1; rowCounter <= 15; rowCounter++)  
      {  
         testTable.Rows.Add(null, "Row #" + rowCounter.ToString());  
      }  
  
      Console.WriteLine("Before Update => ");  
      foreach (DataRow row in testTable.Rows)  
      {  
         Console.WriteLine("   {0} - {1}", row["ID"], row["OtherColumn"]);  
      }  
      Console.WriteLine();  
  
      cmd.CommandText =
        "SELECT ID, OtherColumn FROM SequenceTest_Table";  
      OracleDataAdapter da = new OracleDataAdapter(cmd);  
      da.InsertCommand = new OracleCommand(insertString, conn);  
      da.InsertCommand.Parameters.Add(":ID", OracleType.Int32, 0, "ID");  
      da.InsertCommand.Parameters[0].Direction = ParameterDirection.Output;  
      da.InsertCommand.Parameters.Add(":OtherColumn", OracleType.VarChar, 255, "OtherColumn");  
      da.InsertCommand.UpdatedRowSource = UpdateRowSource.OutputParameters;  
      da.UpdateBatchSize = 10;  
  
      da.Update(testTable);  
  
      Console.WriteLine("After Update => ");  
      foreach (DataRow row in testTable.Rows)  
      {  
         Console.WriteLine("   {0} - {1}", row["ID"], row["OtherColumn"]);  
      }  
      // Close the connection.  
      conn.Close();  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também

- [Oracle e ADO.NET](oracle-and-adonet.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
