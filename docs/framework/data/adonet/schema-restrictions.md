---
description: 'Saiba mais sobre: restrições de esquema'
title: Restrições de esquema
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 73d2980e-e73c-4987-913a-8ddc93d09144
ms.openlocfilehash: 74ddfe5b8aaf9b8193e0c0b2a929ccde333eac26
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99719039"
---
# <a name="schema-restrictions"></a>Restrições de esquema

O segundo parâmetro opcional do método **GetSchema** são as restrições usadas para limitar a quantidade de informações de esquema retornadas, e é transmitido para o método **GetSchema** como uma matriz de cadeias de caracteres. A posição na matriz determina os valores que podem se transmitidos, e isso é equivalente ao número da restrição.  
  
 Por exemplo, a tabela a seguir descreve as restrições suportadas pela coleção de esquema "Tables" usando o Provedor de Dados de .NET Framework para SQL Server. As restrições adicionais para as coleções de esquemas do SQL Server são listadas ao final deste tópico.  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
  
## <a name="specifying-restriction-values"></a>Especificando valores de restrição  

 Para usar uma das restrições da coleção de esquemas "Tables", basta criar uma matriz de cadeias de caracteres com quatro elementos e inserir um valor no elemento que corresponde ao número da restrição. Por exemplo, para restringir as tabelas retornadas pelo método **GetSchema** apenas às tabelas no esquema "Sales", defina o segundo elemento da matriz como "Sales" antes de transmiti-lo para o método **GetSchema**.  
  
> [!NOTE]
> As coleções de restrições para `SqlClient` e `OracleClient` têm uma `ParameterName` coluna adicional. A coluna padrão de restrição ainda está disponível para compatibilidade com versões anteriores, mas é ignorada no momento. Consultas parametrizadas em vez da substituição de cadeia de caracteres devem ser usadas para minimizar o risco de um ataque de injeção de SQL ao especificar valores de restrição.  
  
> [!NOTE]
> O número de elementos na matriz precisa ser inferior ou igual ao número de restrições compatíveis com a coleção de esquemas especificada. Caso contrário, uma <xref:System.ArgumentException> será gerada. Pode haver menos do que o número máximo de restrições. As restrições ausentes são consideradas nulas (irrestrito).  
  
 Você pode consultar um provedor gerenciado .NET Framework para determinar a lista de restrições com suporte chamando o método **GetSchema** com o nome da coleção de esquemas de restrições, que é "restrições". Isso retornará uma <xref:System.Data.DataTable> com uma lista de nomes de coleção, os nomes de restrição, os valores de restrição padrão e os números de restrição.  
  
### <a name="example"></a>Exemplo  

 Os exemplos a seguir demonstram como usar o <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> método do .NET Framework provedor de dados para a <xref:System.Data.SqlClient.SqlConnection> classe SQL Server para recuperar informações de esquema sobre todas as tabelas contidas no banco de dados de exemplo **AdventureWorks** e para restringir as informações retornadas para apenas as tabelas no esquema de "vendas":  
  
```vb  
Imports System.Data.SqlClient  
  
Module Module1  
Sub Main()  
  Dim connectionString As String = _  
    "Data Source=(local);Database=AdventureWorks;" & _  
       "Integrated Security=true;";  
  
  Dim restrictions(3) As String  
  Using connection As New SqlConnection(connectionString)  
    connection.Open()  
  
    'Specify the restrictions.  
    restrictions(1) = "Sales"  
    Dim table As DataTable = connection.GetSchema("Tables", _  
       restrictions)  
  
    ' Display the contents of the table.  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Using  
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
    string connectionString =
       "Data Source=(local);Database=AdventureWorks;" +  
       "Integrated Security=true;";  
    using (SqlConnection connection =  
       new SqlConnection(connectionString))  
    {  
        connection.Open();  
  
        // Specify the restrictions.  
        string[] restrictions = new string[4];  
        restrictions[1] = "Sales";  
        System.Data.DataTable table = connection.GetSchema(  
          "Tables", restrictions);  
  
        // Display the contents of the table.  
        foreach (System.Data.DataRow row in table.Rows)  
        {  
            foreach (System.Data.DataColumn col in table.Columns)  
            {  
                Console.WriteLine("{0} = {1}",
                  col.ColumnName, row[col]);  
            }  
            Console.WriteLine("============================");  
        }  
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
  
## <a name="sql-server-schema-restrictions"></a>Restrições de esquema de SQL Server  

 As tabelas a seguir listam as restrições para coleções de esquemas do SQL Server.  
  
### <a name="users"></a>Usuários  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|User_Name|@Name|name|1|  
  
### <a name="databases"></a>Bancos de dados  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Nome|@Name|Nome|1|  
  
### <a name="tables"></a>Tabelas  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Name|TABLE_NAME|3|  
|TableType|@TableType|TABLE_TYPE|4|  
  
### <a name="columns"></a>Colunas  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
|Coluna|@Column|COLUMN_NAME|4|  
  
### <a name="structuredtypemembers"></a>StructuredTypeMembers  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
|Coluna|@Column|COLUMN_NAME|4|  
  
### <a name="views"></a>Exibições  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
  
### <a name="viewcolumns"></a>ViewColumns  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|VIEW_CATALOG|1|  
|Proprietário|@Owner|VIEW_SCHEMA|2|  
|Tabela|@Table|VIEW_NAME|3|  
|Coluna|@Column|COLUMN_NAME|4|  
  
### <a name="procedureparameters"></a>ProcedureParameters  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|SPECIFIC_CATALOG|1|  
|Proprietário|@Owner|SPECIFIC_SCHEMA|2|  
|Nome|@Name|SPECIFIC_NAME|3|  
|Parâmetro|@Parameter|PARAMETER_NAME|4|  
  
### <a name="procedures"></a>Procedimentos  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|SPECIFIC_CATALOG|1|  
|Proprietário|@Owner|SPECIFIC_SCHEMA|2|  
|Nome|@Name|SPECIFIC_NAME|3|  
|Tipo|@Type|ROUTINE_TYPE|4|  
  
### <a name="indexcolumns"></a>IndexColumns  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|db_name()|1|  
|Proprietário|@Owner|user_name()|2|  
|Tabela|@Table|o.name|3|  
|ConstraintName|@ConstraintName|x.name|4|  
|Coluna|@Column|c.name|5|  
  
### <a name="indexes"></a>Índices  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|db_name()|1|  
|Proprietário|@Owner|user_name()|2|  
|Tabela|@Table|o.name|3|  
  
### <a name="userdefinedtypes"></a>UserDefinedTypes  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|assembly_name|@AssemblyName|assemblies.name|1|  
|udt_name|@UDTName|types.assembly_class|2|  
  
### <a name="foreignkeys"></a>ForeignKeys  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|CONSTRAINT_CATALOG|1|  
|Proprietário|@Owner|CONSTRAINT_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
|Nome|@Name|CONSTRAINT_NAME|4|  
  
## <a name="sql-server-2008-schema-restrictions"></a>SQL Server restrições de esquema do 2008  

 As tabelas a seguir listam as restrições para coleções de esquema do SQL Server 2008. Essas restrições são válidas a partir da versão 3,5 SP1 do .NET Framework e SQL Server 2008. Eles não têm suporte em versões anteriores do .NET Framework e SQL Server.  
  
### <a name="columnsetcolumns"></a>ColumnSetColumns  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
  
### <a name="allcolumns"></a>AllColumns  
  
|Nome da restrição|Nome do Parâmetro|Padrão da restrição|Número da restrição|  
|----------------------|--------------------|-------------------------|------------------------|  
|Catálogo|@Catalog|TABLE_CATALOG|1|  
|Proprietário|@Owner|TABLE_SCHEMA|2|  
|Tabela|@Table|TABLE_NAME|3|  
|Coluna|@Column|COLUMN_NAME|4|  
  
## <a name="see-also"></a>Confira também

- [Visão geral do ADO.NET](ado-net-overview.md)
