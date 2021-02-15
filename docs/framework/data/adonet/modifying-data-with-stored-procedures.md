---
description: 'Saiba mais sobre: Modificando dados com procedimentos armazenados'
title: Modificando dados com procedimentos armazenados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7d8e9a46-1af6-4a02-bf61-969d77ae07e0
ms.openlocfilehash: 66a4aa9577c71605bde0152a142a65dfa81a31d7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786219"
---
# <a name="modifying-data-with-stored-procedures"></a>Modificando dados com procedimentos armazenados

Os procedimentos armazenados podem aceitar dados como parâmetros de entrada e podem retornar dados como parâmetros de saída, conjuntos de resultados ou valores de retorno. O exemplo a seguir ilustra como o ADO.NET envia e recebe parâmetros de entrada, parâmetros de saída e valores de retorno. O exemplo insere um novo registro em uma tabela onde a coluna de chave primária é uma coluna de identidade em um banco de dados do SQL Server.  
  
> [!NOTE]
> Se você estiver usando procedimentos armazenados do SQL Server para editar ou excluir dados usando um <xref:System.Data.SqlClient.SqlDataAdapter>, não use SET NOCOUNT ON na definição do procedimento armazenado. Isso faz com que a contagem retornada de linhas afetadas seja zero, o que o `DataAdapter` interpreta como um conflito de simultaneidade. Nesse caso, será gerada uma <xref:System.Data.DBConcurrencyException>.  
  
## <a name="example"></a>Exemplo  

 O exemplo usa o procedimento armazenado a seguir para inserir uma nova categoria na tabela **Northwind** **Categories**. O procedimento armazenado usa o valor da coluna **CategoryName** como um parâmetro de entrada e a função SCOPE_IDENTITY() para recuperar o novo valor do campo de identidade, **CategoryID**, e retorná-lo em um parâmetro de saída. A instrução RETURN usa a @ROWCOUNT função @ para retornar o número de linhas inseridas.  
  
```sql
CREATE PROCEDURE dbo.InsertCategory  
  @CategoryName nvarchar(15),  
  @Identity int OUT  
AS  
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)  
SET @Identity = SCOPE_IDENTITY()  
RETURN @@ROWCOUNT  
```  
  
 O código de exemplo a seguir usa o procedimento armazenado `InsertCategory` mostrado acima como a origem de <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> de <xref:System.Data.SqlClient.SqlDataAdapter>. O parâmetro de saída `@Identity` será refletido em <xref:System.Data.DataSet> após a inserção do registro no banco de dados quando o método `Update` de <xref:System.Data.SqlClient.SqlDataAdapter> for chamado. O código também recupera o valor de retorno.  
  
> [!NOTE]
> Ao usar o <xref:System.Data.OleDb.OleDbDataAdapter> , você deve especificar parâmetros com um <xref:System.Data.ParameterDirection> de **ReturnValue** antes dos outros parâmetros.  
  
 [!code-csharp[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/VB/source.vb#1)]  
  
## <a name="see-also"></a>Confira também

- [Recuperando e modificando dados no ADO.NET](retrieving-and-modifying-data.md)
- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [Executando um comando](executing-a-command.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
