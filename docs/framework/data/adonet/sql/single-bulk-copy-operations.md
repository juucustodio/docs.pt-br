---
description: 'Saiba mais sobre: operações de cópia única em massa'
title: Operações únicas de cópia em massa
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
ms.openlocfilehash: f6b046fbd73ad798f3f9f117eea0b72f46e43b37
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767473"
---
# <a name="single-bulk-copy-operations"></a>Operações únicas de cópia em massa

A abordagem mais simples para a execução de uma operação de cópia em massa do SQL Server é executar uma única operação em um banco de dados. Por padrão, uma operação de cópia em massa é executada como uma operação isolada: a operação de cópia ocorre de forma não transacionada, sem a oportunidade de disponibilizá-la de volta.

> [!NOTE]
> Se você precisar reverter toda ou parte da cópia em massa quando ocorrer um erro, poderá usar uma transação gerenciada <xref:System.Data.SqlClient.SqlBulkCopy> ou executar a operação de cópia em massa dentro de uma transação existente. **SqlBulkCopy** também funcionará com <xref:System.Transactions> se a conexão for inscrita (implícita ou explicitamente) em uma transação de **System.Transactions**.
>
> Para obter mais informações, consulte [operações de cópia em massa e transação](transaction-and-bulk-copy-operations.md).

As etapas gerais para executar uma operação de cópia em massa são:

1. Conectar-se ao servidor de origem e obter os dados a serem copiados. Os dados também podem vir de outras fontes, desde que possam ser recuperados de um objeto <xref:System.Data.IDataReader> ou <xref:System.Data.DataTable>.

2. Conecte-se ao servidor de destino (a menos que você queira que **SqlBulkCopy** estabeleça uma conexão para você).

3. Crie um objeto <xref:System.Data.SqlClient.SqlBulkCopy>, configurando as propriedades necessárias.

4. Defina a propriedade **DestinationTableName** para indicar a tabela de destino para a operação BULK INSERT.

5. Chame um dos métodos **WriteToServer**.

6. Opcionalmente, atualize as propriedades e chame **WriteToServer** novamente, conforme necessário.

7. Chame <xref:System.Data.SqlClient.SqlBulkCopy.Close%2A> ou encapsule as operações de cópia em massa em uma instrução `Using`.

> [!CAUTION]
> É recomendável que os tipos de dados da coluna de origem e destino correspondam. Se os tipos de dados não corresponderem, o **SqlBulkCopy** tentará converter cada valor de origem para o tipo de dados de destino usando as regras empregadas por <xref:System.Data.SqlClient.SqlParameter.Value%2A>. As conversões podem afetar o desempenho e também podem resultar em erros inesperados. Por exemplo, um tipo de dados `Double` pode ser convertido em um tipo de dados `Decimal` na maior parte das vezes, mas não sempre.

## <a name="example"></a>Exemplo

O aplicativo de console a seguir demonstra como carregar dados usando a classe <xref:System.Data.SqlClient.SqlBulkCopy>. Neste exemplo, um <xref:System.Data.SqlClient.SqlDataReader> é usado para copiar dados da tabela **Production.Product** no banco de dados **AdventureWorks** do SQL Server em uma tabela semelhante no mesmo banco de dados.

> [!IMPORTANT]
> Este exemplo não será executado a menos que você tenha criado as tabelas de trabalho conforme descrito em [configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.

[!code-csharp[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/CS/source.cs#1)]
[!code-vb[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/VB/source.vb#1)]

## <a name="performing-a-bulk-copy-operation-using-transact-sql-and-the-command-class"></a>Executando uma operação de cópia em massa usando Transact-SQL e a classe Command

O exemplo a seguir ilustra como usar o método <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> para executar a instrução BULK INSERT.

> [!NOTE]
> O caminho do arquivo da fonte de dados é relativo ao servidor. O processo do servidor deve ter acesso a esse caminho para que a operação de cópia em massa seja bem-sucedida.

```vb
Using connection As SqlConnection = New SqlConnection(connectionString)
Dim queryString As String = _
    "BULK INSERT Northwind.dbo.[Order Details] FROM " & _
    "'f:\mydata\data.tbl' WITH (FORMATFILE='f:\mydata\data.fmt' )"
connection.Open()
SqlCommand command = New SqlCommand(queryString, connection);

command.ExecuteNonQuery()
End Using
```

```csharp
using (SqlConnection connection = New SqlConnection(connectionString))
{
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +
    "FROM 'f:\mydata\data.tbl' " +
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";
connection.Open();
SqlCommand command = new SqlCommand(queryString, connection);

command.ExecuteNonQuery();
}
```

## <a name="see-also"></a>Consulte também

- [Operações de cópia em massa no SQL Server](bulk-copy-operations-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
