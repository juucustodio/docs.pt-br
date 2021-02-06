---
description: 'Saiba mais sobre: UDTs grandes'
title: UDTs grandes
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.openlocfilehash: e1a40330bb48d6320dc96533e764f1b856e0f410
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663177"
---
# <a name="large-udts"></a>UDTs grandes

Os UDTs (tipos definidos pelo usuário) permitem que os desenvolvedores estendam o sistema de tipo escalar do servidor armazenando objetos de CLR (Common Language Runtime) em um banco de dados SQL Server. Os UDTs podem conter vários elementos e ter comportamentos, diferentemente dos tipos de dados de alias tradicionais, que consistem em um único tipo de dados do sistema no SQL Server.  
  
> [!NOTE]
> Você deve instalar o .NET Framework 3.5 SP1 (ou posterior) para se beneficiar do suporte avançado do SqlClient para UDTs grandes.  
  
 Os UDTs eram anteriormente restritas a um tamanho máximo de 8 kilobytes. No SQL Server 2008, essa restrição foi removida para UDTs que têm um formato de <xref:Microsoft.SqlServer.Server.Format.UserDefined>.  
  
 Para obter a documentação completa para tipos definidos pelo usuário, consulte a versão dos Manuais Online do SQL Server relativos à versão do SQL Server que você está usando.  
  
 **Documentação do SQL Server**  
  
1. [Tipos definido pelo usuário CLR](/sql/relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types)  
  
## <a name="retrieving-udt-schemas-using-getschema"></a>Recuperando esquemas de UDT usando GetSchema  

 O método <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> de <xref:System.Data.SqlClient.SqlConnection> retorna informações de esquema de banco de dados em um <xref:System.Data.DataTable>. Para obter mais informações, consulte [SQL Server coleções de esquema](../sql-server-schema-collections.md).  
  
### <a name="getschematable-column-values-for-udts"></a>Valores de coluna de GetSchemaTable para UDTs  

 O método <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> de um <xref:System.Data.SqlClient.SqlDataReader> retorna um <xref:System.Data.DataTable> que descreve os metadados da coluna. A tabela a seguir descreve as diferenças nos metadados da coluna para UDTs grandes entre o SQL Server 2005 e o SQL Server 2008.  
  
|Coluna SqlDataReader|SQL Server 2005|SQL Server 2008 e posterior|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|Varia|Varia|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|Instância UDT|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|Instância UDT|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|O nome de três partes especificado como *Database.SchemaName.TypeName*.|  
|`IsLong`|Varia|Varia|  
  
## <a name="sqldatareader-considerations"></a>Considerações do SqlDataReader  

 O <xref:System.Data.SqlClient.SqlDataReader> foi estendido a partir do SQL Server 2008 para dar suporte à recuperação de UDTs de valores grandes. A forma como as UDT de valores grandes são processadas por um <xref:System.Data.SqlClient.SqlDataReader> dependem da versão do SQL Server que você está usando, bem como do `Type System Version` especificado na cadeia de conexão. Para obter mais informações, consulte <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
 Os seguintes métodos de <xref:System.Data.SqlClient.SqlDataReader> retornarão um <xref:System.Data.SqlTypes.SqlBinary> em vez de uma UDT quando o `Type System Version` for definido como SQL Server 2005:  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
 Os seguintes métodos retornarão uma matriz de `Byte[]` em vez de uma UDT quando o `Type System Version` for definido como SQL Server 2005:  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
 Observe que nenhuma das conversões são feitas para a versão atual do ADO.NET.  
  
## <a name="specifying-sqlparameters"></a>Especificar SqlParameters  

 As propriedades <xref:System.Data.SqlClient.SqlParameter> a seguir foram estendidas para funcionar com UDTs grandes.  
  
|Propriedade SqlParameter|Descrição|  
|---------------------------|-----------------|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|Obtém ou define um objeto que representa o valor do parâmetro. O padrão é nulo. A propriedade pode ser `SqlBinary`, `Byte[]` ou um objeto gerenciado.|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|Obtém ou define um objeto que representa o valor do parâmetro. O padrão é nulo. A propriedade pode ser `SqlBinary`, `Byte[]` ou um objeto gerenciado.|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|Obtém ou define o tamanho do valor do parâmetro a ser resolvido. O valor padrão é 0. A propriedade pode ser um inteiro que representa o tamanho do valor do parâmetro. Para UDTs grandes, pode ser o tamanho real da UDT ou -1 para desconhecido.|  
  
## <a name="retrieving-data-example"></a>Recuperando exemplo de dados  

 O fragmento de código a seguir demonstra como recuperar dados de uma UDT grande. A variável `connectionString` assume uma conexão válida com um banco de dados SQL Server, e a variável `commandString` pressupõe uma instrução SELECT válida com a coluna de chave primária listada primeiro.  
  
```csharp  
using (SqlConnection connection = new SqlConnection(
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
```vb  
Using connection As New SqlConnection( _  
    connectionString, commandString)  
    connection.Open()  
    Dim command As New SqlCommand(commandString, connection)  
    Dim reader As SqlDataReader  
    reader = command.ExecuteReader  
  
    While reader.Read()  
      ' Retrieve the value of the Primary Key column.  
      Dim id As Int32 = reader.GetInt32(0)  
  
      ' Retrieve the value of the UDT.  
      Dim udt As LargeUDT = CType(reader(1), LargeUDT)  
  
     ' You can also use GetSqlValue and GetValue.  
     ' Dim udt As LargeUDT = CType(reader.GetSqlValue(1), LargeUDT)  
     ' Dim udt As LargeUDT = CType(reader.GetValue(1), LargeUDT)  
  
      ' Print values.  
      Console.WriteLine("ID={0} LargeUDT={1}", id, udt)  
    End While  
    reader.Close()  
End Using  
```  
  
## <a name="see-also"></a>Consulte também

- [Configurar parâmetros e tipos de dados de parâmetro](../configuring-parameters-and-parameter-data-types.md)
- [Como recuperar informações de esquema de banco de dados](../retrieving-database-schema-information.md)
- [Mapeamentos de tipos de dados do SQL Server](../sql-server-data-type-mappings.md)
- [Dados binários e de valor grande do SQL Server](sql-server-binary-and-large-value-data.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
