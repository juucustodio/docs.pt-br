---
description: 'Saiba mais sobre: operações de cópia em massa e transação'
title: Operações de transação e de cópia em massa
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.openlocfilehash: 84e7c3c73a7886fff3a7cc16166b78e26e89ca93
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766979"
---
# <a name="transaction-and-bulk-copy-operations"></a>Operações de transação e de cópia em massa

Operações de cópia em massa podem ser executadas como operações isoladas ou como parte de uma transação de várias etapas. Essa última opção permite executar mais de uma operação de cópia em massa dentro da mesma transação, bem como executar outras operações de banco de dados (como inserções, atualizações e exclusões), podendo ainda confirmar ou reverter toda a transação.  
  
 Por padrão, uma operação de cópia em massa é executada como uma operação isolada. A operação de cópia em massa ocorre de forma não transacionada, sem a oportunidade de revertê-la novamente. Se você precisar reverter toda ou parte da cópia em massa quando ocorrer um erro, poderá usar uma <xref:System.Data.SqlClient.SqlBulkCopy> transação gerenciada, executar a operação de cópia em massa dentro de uma transação existente ou ser inscrito em um **System. Transactions** <xref:System.Transactions.Transaction> .  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>Executando uma operação não transacionada de cópia em massa  

 O aplicativo de Console a seguir mostra o que acontece quando uma operação de cópia em massa não transacionada encontra um erro na operação.  
  
 No exemplo, cada tabela de origem e cada tabela de destino incluem uma coluna `Identity` denominada **ProductID**. O código prepara primeiro a tabela de destino excluindo todas as linhas e, em seguida, inserindo uma única linha cuja **ProductID** é conhecida por existir na tabela de origem. Por padrão, um novo valor para a coluna `Identity` é gerado na tabela de destino para cada linha adicionada. Neste exemplo, uma opção é definida quando a conexão é aberta, o que força o processo de carregamento em massa a usar os valores de `Identity` da tabela de origem.  
  
 A operação de cópia em massa é executada com a propriedade <xref:System.Data.SqlClient.SqlBulkCopy.BatchSize%2A> definida como 10. Quando a operação encontra a linha inválida, uma exceção é lançada. Neste primeiro exemplo, a operação de cópia em massa é não transacionada. Todos os lotes copiados até o ponto do erro são confirmados; o lote que contém a chave duplicada é revertido e a operação de cópia em massa é interrompida antes de processar todos os outros lotes.  
  
> [!NOTE]
> Este exemplo não será executado a menos que você tenha criado as tabelas de trabalho conforme descrito em [configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
 [!code-csharp[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/VB/source.vb#1)]  
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>Executando uma operação dedicada de cópia em massa em uma transação  

 Por padrão, uma operação de cópia em massa é sua própria transação. Quando quiser executar uma operação de cópia em massa dedicada, crie uma instância do <xref:System.Data.SqlClient.SqlBulkCopy> com uma cadeia de conexão ou use um objeto <xref:System.Data.SqlClient.SqlConnection> existente sem uma transação ativa. Em cada cenário, a operação de cópia em massa cria e, em seguida, confirma ou reverte a transação.  
  
 Você pode especificar explicitamente a opção <xref:System.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> no construtor de classe <xref:System.Data.SqlClient.SqlBulkCopy> para explicitamente fazer com que uma operação de cópia em massa seja executada em sua própria transação, fazendo com que cada lote da operação de cópia em massa seja executado dentro de uma transação separada.  
  
> [!NOTE]
> Como lotes diferentes são executados em diferentes transações, se ocorrer um erro durante a operação de cópia em massa, todas as linhas no lote atual serão revertidas, mas as linhas de lotes anteriores permanecerão no banco de dados.  
  
 O aplicativo de console a seguir é semelhante ao exemplo anterior, com uma exceção: neste exemplo, a operação de cópia em massa gerencia suas próprias transações. Todos os lotes copiados até o ponto do erro são confirmados; o lote que contém a chave duplicada é revertido e a operação de cópia em massa é interrompida antes de processar todos os outros lotes.  
  
> [!IMPORTANT]
> Este exemplo não será executado a menos que você tenha criado as tabelas de trabalho conforme descrito em [configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
 [!code-csharp[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/VB/source.vb#1)]  
  
## <a name="using-existing-transactions"></a>Usando transações existentes  

 É possível especificar um objeto <xref:System.Data.SqlClient.SqlTransaction> existente como um parâmetro em um construtor <xref:System.Data.SqlClient.SqlBulkCopy>. Nessa situação, a operação de cópia em massa é executada em uma transação existente e nenhuma alteração é feita ao estado da transação (isto é, ela não é confirmada nem anulada). Isso permite que um aplicativo inclua a operação de cópia em massa em uma transação com outras operações de banco de dados. No entanto, uma exceção será lançada caso você não especifique um objeto <xref:System.Data.SqlClient.SqlTransaction>, passe uma referência nula e caso a conexão tenha uma transação ativa.  
  
 Caso precise reverter toda a operação de cópia em massa porque ocorreu um erro. Ou caso a cópia em massa deva ser executada como parte de um processo maior que pode ser revertido, será possível fornecer um objeto <xref:System.Data.SqlClient.SqlTransaction> para o construtor <xref:System.Data.SqlClient.SqlBulkCopy>.  
  
 O aplicativo de console a seguir é semelhante para o primeiro exemplo (não transacionado), com uma exceção: neste exemplo, a operação de cópia em massa está incluída em uma transação maior, externa. Quando ocorre o erro de violação de chave primária, a transação inteira é revertida e nenhuma linha é adicionada à tabela de destino.  
  
> [!IMPORTANT]
> Este exemplo não será executado a menos que você tenha criado as tabelas de trabalho conforme descrito em [configuração de exemplo de cópia em massa](bulk-copy-example-setup.md). Esse código é fornecido para demonstrar a sintaxe para usar somente **SqlBulkCopy**. Se as tabelas de origem e destino estiverem localizadas na mesma instância do SQL Server, será mais fácil e mais rápido usar uma instrução `INSERT … SELECT` do Transact-SQL para copiar os dados.  
  
 [!code-csharp[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/VB/source.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Operações de cópia em massa no SQL Server](bulk-copy-operations-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
