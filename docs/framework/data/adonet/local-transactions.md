---
description: 'Saiba mais sobre: transações locais'
title: Transações locais
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
ms.openlocfilehash: 998024a6b08ec9cb97c8bb8dbbe2c9d17f38f350
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681637"
---
# <a name="local-transactions"></a>Transações locais

As transações do ADO.NET são usadas quando você deseja associar várias tarefas para que elas sejam executadas como uma só unidade de trabalho. Por exemplo, imagine que um aplicativo executa duas tarefas. Primeiro, ele atualiza uma tabela com informações sobre pedidos. Em seguida, ele atualiza uma tabela que contém informações de inventário, debitando os itens pedidos. Se uma das tarefas falhar, as duas atualizações serão revertidas.  
  
## <a name="determining-the-transaction-type"></a>Determinando o tipo de transação  

 Uma transação é considerada local quando é monofásica e é tratada diretamente pelo banco de dados. Uma transação é considerada distribuída quando é coordenada por um monitor de transação e usa mecanismos à prova de falhas (como o protocolo 2PC) na resolução das transações.  
  
 Cada um dos provedores de dados de .NET Framework tem seu próprio `Transaction` objeto para executar transações locais. Se você precisar executar uma transação em um banco de dados do SQL Server, selecione uma transação <xref:System.Data.SqlClient>. Para uma transação Oracle, use o provedor <xref:System.Data.OracleClient>. Além disso, há uma classe <xref:System.Data.Common.DbTransaction> que está disponível para a criação de um código independente de provedor que exige transações.  
  
> [!NOTE]
> As transações são mais eficientes quando são executadas no servidor. Se você estiver trabalhando com um banco de dados do SQL Server que faz uso extensivo de transações explícitas, considere criá-las como procedimentos armazenados usando a instrução Transact-SQL BEGIN TRANSACTION.
  
## <a name="performing-a-transaction-using-a-single-connection"></a>Executando uma transação com uma única conexão  

 No ADO.NET, você controla as transações com o objeto `Connection`. É possível iniciar uma transação local com o método `BeginTransaction`. Depois de iniciar uma transação, você pode inscrever um comando nessa transação com a propriedade `Transaction` de um objeto `Command`. Em seguida, você poderá confirmar ou reverter todas as modificações feitas na fonte de dados com base no êxito ou na falha dos componentes de transação.  
  
> [!NOTE]
> O método `EnlistDistributedTransaction` não deve ser usado para uma transação local.  
  
 O escopo da transação é limitado à conexão. O exemplo a seguir executa uma transação explícita que consiste em dois comandos separados no bloco `try`. Os comandos executam instruções INSERT na tabela Production. ScrapReason da AdventureWorks SQL Server banco de dados de exemplo, que são confirmadas se nenhuma exceção for gerada. O código no bloco `catch` reverterá a transação se uma exceção for lançada. Se a transação for anulada ou a conexão for fechada antes de a transação ser concluída, a transação será automaticamente revertida.  
  
## <a name="example"></a>Exemplo  

 Siga estas etapas para executar uma transação.  
  
1. Chame o método <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> do objeto <xref:System.Data.SqlClient.SqlConnection> para marcar o início da transação. O método <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> retorna uma referência à transação. Essa referência é atribuída aos objetos <xref:System.Data.SqlClient.SqlCommand> inscritos na transação.  
  
2. Atribua o objeto `Transaction` à propriedade <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> de <xref:System.Data.SqlClient.SqlCommand> a ser executado. Se um comando for executado em uma conexão com uma transação ativa, e o objeto `Transaction` não tiver sido atribuído à propriedade `Transaction` do objeto `Command`, uma exceção será gerada.  
  
3. Execute os comandos necessários.  
  
4. Chame o método <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> do objeto <xref:System.Data.SqlClient.SqlTransaction> para concluir a transação, ou chame o método <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> para finalizar a transação. Se a conexão for fechada ou descartada antes do método <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> ou <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A> ser executado, a transação será revertida.  
  
 O exemplo de código a seguir demonstra a lógica transacional usando ADO.NET com Microsoft SQL Server.  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Transações e simultaneidade](transactions-and-concurrency.md)
- [Transações distribuídas](distributed-transactions.md)
- [Integração de System.Transactions com o SQL Server](system-transactions-integration-with-sql-server.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
