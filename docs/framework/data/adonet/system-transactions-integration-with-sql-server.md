---
description: 'Saiba mais sobre: integração de System. Transactions com o SQL Server'
title: Integração de System.Transactions com o SQL Server
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b555544e-7abb-4814-859b-ab9cdd7d8716
ms.openlocfilehash: 977ff18600256613dabc0212c2f7aa1bc2650408
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766771"
---
# <a name="systemtransactions-integration-with-sql-server"></a>Integração de System.Transactions com o SQL Server

O .NET Framework versão 2,0 introduziu uma estrutura de transação que pode ser acessada por meio do <xref:System.Transactions> namespace. Essa estrutura expõe transações de uma maneira totalmente integrada no .NET Framework, incluindo ADO.NET.  
  
 Além dos aprimoramentos de programação, o <xref:System.Transactions> e o ADO.NET podem trabalhar em conjunto para coordenar otimizações quando você trabalha com transações. Uma transação passível de promoção é uma transação leve (local) que pode ser promovida automaticamente a uma transação totalmente distribuída, conforme necessário.  
  
 A partir do ADO.NET 2,0, o <xref:System.Data.SqlClient> oferece suporte a transações de promoção quando você trabalha com SQL Server. Uma transação passível de promoção não chama a sobrecarga adicional de uma transação distribuída a menos que a sobrecarga adicional seja necessária. As transações passíveis de promoção são automáticas e não exigem nenhuma intervenção do desenvolvedor.  
  
 As transações de promoçãotable só estão disponíveis quando você usa o .NET Framework Provedor de Dados para SQL Server ( `SqlClient` ) com SQL Server.  
  
## <a name="creating-promotable-transactions"></a>Criando transações de promotable  

 O provedor de .NET Framework para SQL Server fornece suporte para transações de promoção, que são manipuladas por meio das classes no <xref:System.Transactions> namespace .NET Framework. As transações passíveis de promoção otimizam as transações distribuídas por meio da criação de uma transação distribuída até que seja necessária. Se apenas um gerenciador de recursos for necessário, não ocorrerá nenhuma transação distribuída.  
  
> [!NOTE]
> Em um cenário parcialmente confiável, a <xref:System.Transactions.DistributedTransactionPermission> é necessária quando uma transação é promovida para uma transação distribuída.  
  
## <a name="promotable-transaction-scenarios"></a>Cenários de transação de promoção  

 As transações distribuídas normalmente consomem recursos significativos do sistema, sendo gerenciadas pelo MS DTC (Coordenador de Transações Distribuídas da Microsoft), que integra todos os gerenciadores de recursos acessados na transação. Uma transação passível de promoção é uma forma especial de uma transação <xref:System.Transactions> que delega efetivamente o trabalho para uma simples transação do SQL Server. O <xref:System.Transactions>, o <xref:System.Data.SqlClient> e o SQL Server coordenam o trabalho envolvido no tratamento da transação, promovendo-a para uma transação distribuída completa, conforme necessário.  
  
 A vantagem de usar transações passíveis de promoção é que, quando uma conexão é aberta com uma transação <xref:System.Transactions.TransactionScope> ativa e não há nenhuma outra conexão aberta, a transação é confirmada como uma transação leve, em vez de gerar a sobrecarga adicional de uma transação distribuída completa.  
  
### <a name="connection-string-keywords"></a>Palavras-chave de cadeia de conexão  

 A propriedade <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> dá suporte a uma palavra-chave, `Enlist`, que indica se <xref:System.Data.SqlClient> detectará contextos transacionais e inscreverá automaticamente a conexão em uma transação distribuída. Se `Enlist=true`, a conexão será inscrita automaticamente no contexto de transação atual do thread de abertura. Se `Enlist=false`, a conexão `SqlClient` não interagirá com uma transação distribuída. O valor padrão de `Enlist` é true. Se `Enlist` não estiver especificado na cadeia de conexão, a conexão será inscrita automaticamente em uma transação distribuída, caso uma seja detectada no momento em que a conexão é aberta.  
  
 As palavras-chave `Transaction Binding` em uma cadeia de conexão <xref:System.Data.SqlClient.SqlConnection> controlam a associação da conexão com uma transação `System.Transactions` inscrita. Ela também está disponível por meio da propriedade <xref:System.Data.SqlClient.SqlConnectionStringBuilder.TransactionBinding%2A> de um <xref:System.Data.SqlClient.SqlConnectionStringBuilder>.  
  
 A tabela a seguir descreve os valores possíveis.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|Desassociação implícita|O padrão. A conexão é desanexada da transação quando ela é encerrada, voltando para o modo de confirmação automática.|  
|Desassociação explícita|A conexão permanece anexada à transação até que a transação seja fechada. A conexão falhará se a transação associada não estiver ativa ou não corresponder a <xref:System.Transactions.Transaction.Current%2A>.|  
  
## <a name="using-transactionscope"></a>Como usar TransactionScope  

 Uma classe <xref:System.Transactions.TransactionScope> torna um bloco de código transacional inscrevendo implicitamente conexões em uma transação distribuída. Você precisará chamar o método <xref:System.Transactions.TransactionScope.Complete%2A> no final do bloco <xref:System.Transactions.TransactionScope> antes de deixá-lo. Deixar o bloco invoca o método <xref:System.Transactions.TransactionScope.Dispose%2A>. Se tiver sido gerada uma exceção que faz o código deixar o escopo, a transação será considerada anulada.  
  
 Recomendamos que você use um bloco `using` para garantir que <xref:System.Transactions.TransactionScope.Dispose%2A> seja chamado no objeto <xref:System.Transactions.TransactionScope> quando o bloco using for encerrado. Uma falha ao confirmar ou reverter transações pendentes pode diminuir muito o desempenho, pois o tempo limite padrão para o <xref:System.Transactions.TransactionScope> é de um minuto. Se você não usar uma instrução `using`, deverá executar todo o trabalho em um bloco `Try` e chamar explicitamente o método <xref:System.Transactions.TransactionScope.Dispose%2A> no bloco `Finally`.  
  
 Se ocorrer uma exceção no <xref:System.Transactions.TransactionScope>, a transação será marcada como inconsistente e abandonada. Ela será revertida quando o <xref:System.Transactions.TransactionScope> for descartado. Se nenhuma exceção ocorrer, as transações participantes serão confirmadas.  
  
> [!NOTE]
> Por padrão, a classe `TransactionScope` cria uma transação com um <xref:System.Transactions.Transaction.IsolationLevel%2A> de `Serializable`. Dependendo do seu aplicativo, talvez você queira considerar abaixar o nível de isolamento para evitar uma contenção elevada em seu aplicativo.  
  
> [!NOTE]
> Recomendamos executar apenas atualizações, inserções e exclusões em transações distribuídas, pois elas consomem recursos de banco de dados significativos. As instruções SELECT poderão bloquear recursos do banco de dados desnecessariamente e, em alguns cenários, você poderá precisar usar transações para seleções. Qualquer trabalho que não seja do banco de dados deve ser executado fora do escopo da transação, a menos que envolva outros gerenciadores de recursos transacionados. Apesar de uma exceção no escopo da transação evitar que a transação seja confirmada, a classe <xref:System.Transactions.TransactionScope> não tem provisão para reverter as alterações que o código tenha feito fora do escopo da própria transação. Se você precisar executar alguma ação ao reverter a ação, escreva sua implementação da interface <xref:System.Transactions.IEnlistmentNotification> e inscreva-se na transação explicitamente.  
  
## <a name="example"></a>Exemplo  

 O uso de <xref:System.Transactions> exige que você tenha uma referência a System.Transactions.dll.  
  
 A função a seguir demonstra como criar uma transação passível de promoção em duas instâncias diferentes do SQL Server, representadas por dois objetos <xref:System.Data.SqlClient.SqlConnection> diferentes, que são encapsulados em um bloco <xref:System.Transactions.TransactionScope>. O código cria o <xref:System.Transactions.TransactionScope> bloco com uma `using` instrução e abre a primeira conexão, que a lista automaticamente no <xref:System.Transactions.TransactionScope> . A transação é inscrita inicialmente como uma transação lightweight, não uma transação distribuída completa. A segunda conexão será inscrita no <xref:System.Transactions.TransactionScope> somente se o comando na primeira conexão não gerar uma exceção. Quando a segunda conexão é aberta, a transação é automaticamente promovida para uma transação distribuída completa. O <xref:System.Transactions.TransactionScope.Complete%2A> método é invocado, que confirma a transação somente se nenhuma exceção tiver sido gerada. Se uma exceção for gerada em algum ponto no bloco <xref:System.Transactions.TransactionScope>, `Complete` não será chamado, e a transação distribuída será revertida quando o <xref:System.Transactions.TransactionScope> for descartado no final do bloco `using`.  
  
```csharp  
// This function takes arguments for the 2 connection strings and commands in order  
// to create a transaction involving two SQL Servers. It returns a value > 0 if the  
// transaction committed, 0 if the transaction rolled back. To test this code, you can
// connect to two different databases on the same server by altering the connection string,  
// or to another RDBMS such as Oracle by altering the code in the connection2 code block.  
static public int CreateTransactionScope(  
    string connectString1, string connectString2,  
    string commandText1, string commandText2)  
{  
    // Initialize the return value to zero and create a StringWriter to display results.  
    int returnValue = 0;  
    System.IO.StringWriter writer = new System.IO.StringWriter();  
  
    // Create the TransactionScope in which to execute the commands, guaranteeing  
    // that both commands will commit or roll back as a single unit of work.  
    using (TransactionScope scope = new TransactionScope())  
    {  
        using (SqlConnection connection1 = new SqlConnection(connectString1))  
        {  
            try  
            {  
                // Opening the connection automatically enlists it in the
                // TransactionScope as a lightweight transaction.  
                connection1.Open();  
  
                // Create the SqlCommand object and execute the first command.  
                SqlCommand command1 = new SqlCommand(commandText1, connection1);  
                returnValue = command1.ExecuteNonQuery();  
                writer.WriteLine("Rows to be affected by command1: {0}", returnValue);  
  
                // if you get here, this means that command1 succeeded. By nesting  
                // the using block for connection2 inside that of connection1, you  
                // conserve server and network resources by opening connection2
                // only when there is a chance that the transaction can commit.
                using (SqlConnection connection2 = new SqlConnection(connectString2))  
                    try  
                    {  
                        // The transaction is promoted to a full distributed  
                        // transaction when connection2 is opened.  
                        connection2.Open();  
  
                        // Execute the second command in the second database.  
                        returnValue = 0;  
                        SqlCommand command2 = new SqlCommand(commandText2, connection2);  
                        returnValue = command2.ExecuteNonQuery();  
                        writer.WriteLine("Rows to be affected by command2: {0}", returnValue);  
                    }  
                    catch (Exception ex)  
                    {  
                        // Display information that command2 failed.  
                        writer.WriteLine("returnValue for command2: {0}", returnValue);  
                        writer.WriteLine("Exception Message2: {0}", ex.Message);  
                    }  
            }  
            catch (Exception ex)  
            {  
                // Display information that command1 failed.  
                writer.WriteLine("returnValue for command1: {0}", returnValue);  
                writer.WriteLine("Exception Message1: {0}", ex.Message);  
            }  
        }  
  
        // If an exception has been thrown, Complete will not
        // be called and the transaction is rolled back.  
        scope.Complete();  
    }  
  
    // The returnValue is greater than 0 if the transaction committed.  
    if (returnValue > 0)  
    {  
        writer.WriteLine("Transaction was committed.");  
    }  
    else  
    {  
        // You could write additional business logic here, notify the caller by  
        // throwing a TransactionAbortedException, or log the failure.  
        writer.WriteLine("Transaction rolled back.");  
    }  
  
    // Display messages.  
    Console.WriteLine(writer.ToString());  
  
    return returnValue;  
}  
```  
  
```vb  
' This function takes arguments for the 2 connection strings and commands in order  
' to create a transaction involving two SQL Servers. It returns a value > 0 if the  
' transaction committed, 0 if the transaction rolled back. To test this code, you can
' connect to two different databases on the same server by altering the connection string,  
' or to another RDBMS such as Oracle by altering the code in the connection2 code block.  
Public Function CreateTransactionScope( _  
  ByVal connectString1 As String, ByVal connectString2 As String, _  
  ByVal commandText1 As String, ByVal commandText2 As String) As Integer  
  
    ' Initialize the return value to zero and create a StringWriter to display results.  
    Dim returnValue As Integer = 0  
    Dim writer As System.IO.StringWriter = New System.IO.StringWriter  
  
    ' Create the TransactionScope in which to execute the commands, guaranteeing  
    ' that both commands will commit or roll back as a single unit of work.  
    Using scope As New TransactionScope()  
        Using connection1 As New SqlConnection(connectString1)  
            Try  
                ' Opening the connection automatically enlists it in the
                ' TransactionScope as a lightweight transaction.  
                connection1.Open()  
  
                ' Create the SqlCommand object and execute the first command.  
                Dim command1 As SqlCommand = New SqlCommand(commandText1, connection1)  
                returnValue = command1.ExecuteNonQuery()  
                writer.WriteLine("Rows to be affected by command1: {0}", returnValue)  
  
                ' If you get here, this means that command1 succeeded. By nesting  
                ' the Using block for connection2 inside that of connection1, you  
                ' conserve server and network resources by opening connection2
                ' only when there is a chance that the transaction can commit.
                Using connection2 As New SqlConnection(connectString2)  
                    Try  
                        ' The transaction is promoted to a full distributed  
                        ' transaction when connection2 is opened.  
                        connection2.Open()  
  
                        ' Execute the second command in the second database.  
                        returnValue = 0  
                        Dim command2 As SqlCommand = New SqlCommand(commandText2, connection2)  
                        returnValue = command2.ExecuteNonQuery()  
                        writer.WriteLine("Rows to be affected by command2: {0}", returnValue)  
  
                    Catch ex As Exception  
                        ' Display information that command2 failed.  
                        writer.WriteLine("returnValue for command2: {0}", returnValue)  
                        writer.WriteLine("Exception Message2: {0}", ex.Message)  
                    End Try  
                End Using  
  
            Catch ex As Exception  
                ' Display information that command1 failed.  
                writer.WriteLine("returnValue for command1: {0}", returnValue)  
                writer.WriteLine("Exception Message1: {0}", ex.Message)  
            End Try  
        End Using  
  
        ' If an exception has been thrown, Complete will
        ' not be called and the transaction is rolled back.  
        scope.Complete()  
    End Using  
  
    ' The returnValue is greater than 0 if the transaction committed.  
    If returnValue > 0 Then  
        writer.WriteLine("Transaction was committed.")  
    Else  
        ' You could write additional business logic here, notify the caller by  
        ' throwing a TransactionAbortedException, or log the failure.  
       writer.WriteLine("Transaction rolled back.")  
     End If  
  
    ' Display messages.  
    Console.WriteLine(writer.ToString())  
  
    Return returnValue  
End Function  
```  
  
## <a name="see-also"></a>Confira também

- [Transações e simultaneidade](transactions-and-concurrency.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
