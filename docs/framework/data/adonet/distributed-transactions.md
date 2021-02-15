---
description: 'Saiba mais sobre: transações distribuídas'
title: Transações distribuídas
ms.date: 03/30/2017
ms.assetid: 718b257c-bcb2-408e-b004-a7b0adb1c176
ms.openlocfilehash: 611fe4e2139e69e9501a3ea04a6aa62425e06728
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651113"
---
# <a name="distributed-transactions"></a>Transações distribuídas

Uma transação é um conjunto de tarefas relacionadas que é bem-sucedida (confirmação) ou falha (anulação) como uma unidade, entre outras coisas. Uma *transação distribuída* é uma transação que afeta vários recursos. Para que uma transação distribuída seja confirmada, todos os participantes devem garantir que qualquer alteração nos dados será permanente. As alterações devem persistir mesmo que haja falhas do sistema ou outros eventos imprevisíveis. Mesmo se um único participante não fizer essa garantia, a transação inteira falhará e todas as alterações aos dados dentro do escopo da transação serão revertidas.  
  
> [!NOTE]
> Uma exceção será gerada se você tentar confirmar ou reverter uma transação se um `DataReader` for iniciado enquanto a transação estiver ativa.  
  
## <a name="working-with-systemtransactions"></a>Trabalhando com System.Transactions  

 No .NET Framework, as transações distribuídas são gerenciadas por meio da API no namespace <xref:System.Transactions>. A API <xref:System.Transactions> delegará a manipulação da transação distribuída para um monitor de transação como o Coordenador de transações distribuídas da Microsoft (DTC) quando vários gerentes de recurso persistentes estão envolvidos. Para obter mais informações, confira os [Conceitos básicos da transação](../transactions/transaction-fundamentals.md).  
  
 O ADO.NET 2.0 introduziu o suporte para inscrição em uma transação distribuída usando o método `EnlistTransaction`, que inscreve uma conexão em uma instância <xref:System.Transactions.Transaction>. Em versões anteriores do ADO.NET, a inscrição explícita em transações distribuídas foi realizada usando o método `EnlistDistributedTransaction` de uma conexão para inscrever uma conexão em uma instância <xref:System.EnterpriseServices.ITransaction>, que não tem suporte para compatibilidade com versões anteriores. Para obter mais informações sobre as transações de serviços corporativos, confira [Interoperabilidade com os serviços corporativos e as transações COM+](../transactions/interoperability-with-enterprise-services-and-com-transactions.md).  
  
 Ao usar uma transação <xref:System.Transactions> com o provedor do .NET Framework para SQL Server em um banco de dados do SQL Server, um <xref:System.Transactions.Transaction> leve será usado automaticamente. A transação pode então ser promovida a uma transação distribuída completa conforme o necessário. Para obter mais informações, consulte [integração de System. Transactions com o SQL Server](system-transactions-integration-with-sql-server.md).  
  
> [!NOTE]
> O número máximo de transações distribuídas no qual um banco de dados Oracle pode participar ao mesmo tempo é definido como 10 por padrão. Após a 10ª transação durante a conexão com um banco de dados Oracle, uma exceção é gerada. A Oracle não oferece suporte a `DDL` dentro de uma transação distribuída.  
  
## <a name="automatically-enlisting-in-a-distributed-transaction"></a>Automaticamente inscrevendo em uma transação distribuída  

 A inscrição automática é a maneira padrão (e preferida) de integrar conexões ADO.NET com `System.Transactions`. Um objeto de conexão será inscrito automaticamente em uma transação distribuída existente se ele determinar que uma transação está ativa, o que, nos termos do `System.Transaction`, significa que `Transaction.Current` não é nulo. A inscrição automática de transação ocorre quando a conexão é aberta. Isso não ocorrerá depois disso, mesmo que um comando seja executado dentro de um escopo de transação. Você pode desativar a inscrição automática em transações existentes especificando `Enlist=false` como um parâmetro de cadeia de conexão para um <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> ou `OLE DB Services=-7` como um parâmetro de cadeia de conexão para um <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A?displayProperty=nameWithType>. Para obter mais informações sobre Oracle e os parâmetros da cadeia de conexão ODBC, consulte <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A?displayProperty=nameWithType> e <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A?displayProperty=nameWithType>.  
  
## <a name="manually-enlisting-in-a-distributed-transaction"></a>Inscrevendo manualmente em uma transação distribuída  

 Se a inscrição automática estiver desativada ou se você precisar inscrever uma transação que foi iniciada depois que a conexão foi aberta, você poderá inscrever-se em uma transação distribuída existente usando o método `EnlistTransaction` do objeto <xref:System.Data.Common.DbConnection> para o provedor com o qual você está trabalhando. A inscrição em uma transação atribuída existente garante que, se a transação for confirmada ou revertida, as alterações feitas pelo código na fonte de dados também serão confirmadas ou revertidas.  
  
 Inscrever-se em transações distribuídas é aplicável principalmente ao agrupar objetos de negócios. Se um objeto de negócios é agrupado com uma conexão aberta, a inscrição automática da transação ocorre somente quando essa conexão está aberta. Se várias transações são executadas usando o objeto comercial agrupado, a conexão aberta para esse objeto não se inscreverá automaticamente em transações iniciadas recentemente. Nesse caso, você pode desabilitar a inscrição automática de transação para a conexão e inscrever a conexão nas transações usando `EnlistTransaction`.  
  
 `EnlistTransaction` usa um só argumento do tipo <xref:System.Transactions.Transaction> que é uma referência para a transação existente. Após chamar o método `EnlistTransaction` da conexão, as modificações feitas na fonte de dados usando a conexão serão incluídas na transação. Passar um valor nulo cancela a inscrição da conexão de sua inscrição de transação distribuída atual. Observe que a conexão deve ser aberta antes de chamar `EnlistTransaction`.  
  
> [!NOTE]
> Assim que uma conexão é inscrita explicitamente em uma transação, ela não pode ter a inscrição cancelada nem ser inscrita em outra transação até a primeira transação terminar.  
  
> [!CAUTION]
> `EnlistTransaction` gera uma exceção se a conexão já tiver começado uma transação usando o método <xref:System.Data.Common.DbConnection.BeginTransaction%2A> da conexão. No entanto, se a transação for uma transação local iniciada na fonte de dados (por exemplo, executando a instrução BEGIN TRANSACTION explicitamente usando uma <xref:System.Data.SqlClient.SqlCommand>), o `EnlistTransaction` reverterá a transação local e se inscreverá na transação distribuída existente conforme o solicitado. Você não receberá o aviso de que a transação local foi revertida e deverá gerenciar as transações locais não iniciadas usando <xref:System.Data.Common.DbConnection.BeginTransaction%2A>. Se você estiver usando o provedor de dados .NET Framework para SQL Server (`SqlClient`) com SQL Server, uma tentativa de inscrição gerará uma exceção. Todos os outros casos permanecerão despercebidos.  
  
## <a name="promotable-transactions-in-sql-server"></a>Transações passíveis de promoção no SQL Server  

 O SQL Server oferece suporte a transações passíveis de promoção nas quais uma transação leve local pode ser automaticamente promovida para uma transação distribuída somente se isso for necessário. Uma transação passível de promoção não chama a sobrecarga adicional de uma transação distribuída a menos que a sobrecarga adicional seja necessária. Para obter mais informações e um exemplo de código, consulte [integração de System. Transactions com o SQL Server](system-transactions-integration-with-sql-server.md).  
  
## <a name="configuring-distributed-transactions"></a>Configurando transações distribuídas  

 Você talvez precise habilitar o MS DTC na rede para usar transações distribuídas. Se tiver o Firewall do Windows habilitado, você deverá permitir que o serviço do MS DTC use a rede ou abra a porta do MS DTC.  
  
## <a name="see-also"></a>Veja também

- [Transações e simultaneidade](transactions-and-concurrency.md)
- [Integração de System.Transactions com o SQL Server](system-transactions-integration-with-sql-server.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
