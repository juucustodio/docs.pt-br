---
description: 'Saiba mais sobre: eventos de conexão'
title: Eventos de conexão
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5a29de74-acfc-4134-8616-829dd7ce0710
ms.openlocfilehash: fcf131e41ce90db11e84fd241744e348f4ca739e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663801"
---
# <a name="connection-events"></a>Eventos de conexão

Todos os provedores de dados de .NET Framework têm objetos de **conexão** com dois eventos que você pode usar para recuperar mensagens informativas de uma fonte de dados ou para determinar se o estado de uma **conexão** foi alterado. A tabela a seguir descreve os eventos do objeto **Connection**.  
  
|Evento|Descrição|  
|-----------|-----------------|  
|**InfoMessage**|Ocorre quando uma mensagem informativa é retornada de uma fonte de dados. As mensagens informativas são as mensagens de uma fonte de dados que não resultam em uma exceção sendo lançada.|  
|**StateChange**|Ocorre quando o estado de **Connection** é alterado.|  
  
## <a name="working-with-the-infomessage-event"></a>Trabalhando com o evento InfoMessage  

 Você pode recuperar avisos e mensagens informativas de uma fonte de dados do SQL Server usando o evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> do objeto <xref:System.Data.SqlClient.SqlConnection>. Os erros retornados da fonte de dados com um nível de severidade de 11 a 16 geram uma exceção. No entanto, o evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> pode ser usado para obter as mensagens da fonte de dados que não estão associadas a um erro. No caso do Microsoft SQL Server, qualquer erro com uma severidade de 10 ou menos é considerado uma mensagem informativa e podem ser capturado usando o evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage>. Para saber mais, leia o artigo [Severidade dos erros do Mecanismo de Banco de Dados](/sql/relational-databases/errors-events/database-engine-error-severities).
  
 O evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> recebe um objeto <xref:System.Data.SqlClient.SqlInfoMessageEventArgs> que contém, em sua propriedade **Errors**, uma coleção das mensagens da fonte de dados. Você pode consultar os objetos **Error** nessa coleção para ver o número do erro e o texto da mensagem, assim como a origem do erro. O provedor de dados .NET Framework para SQL Server também inclui detalhes sobre o banco de dados, o procedimento armazenado e o número da linha da qual a mensagem veio.  
  
### <a name="example"></a>Exemplo  

 O exemplo de código a seguir mostra como adicionar um manipulador de eventos para o evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage>.  
  
```vb  
' Assumes that connection represents a SqlConnection object.  
  AddHandler connection.InfoMessage, _  
    New SqlInfoMessageEventHandler(AddressOf OnInfoMessage)  
  
Private Shared Sub OnInfoMessage(sender As Object, _  
  args As SqlInfoMessageEventArgs)  
  Dim err As SqlError  
  For Each err In args.Errors  
    Console.WriteLine("The {0} has received a severity {1}, _  
       state {2} error number {3}\n" & _  
      "on line {4} of procedure {5} on server {6}:\n{7}", _  
      err.Source, err.Class, err.State, err.Number, err.LineNumber, _  
    err.Procedure, err.Server, err.Message)  
  Next  
End Sub  
```  
  
```csharp  
// Assumes that connection represents a SqlConnection object.  
  connection.InfoMessage +=
    new SqlInfoMessageEventHandler(OnInfoMessage);  
  
protected static void OnInfoMessage(  
  object sender, SqlInfoMessageEventArgs args)  
{  
  foreach (SqlError err in args.Errors)  
  {  
    Console.WriteLine(  
  "The {0} has received a severity {1}, state {2} error number {3}\n" +  
  "on line {4} of procedure {5} on server {6}:\n{7}",  
   err.Source, err.Class, err.State, err.Number, err.LineNumber,
   err.Procedure, err.Server, err.Message);  
  }  
}  
```  
  
## <a name="handling-errors-as-infomessages"></a>Tratando erros como InfoMessages  

 O evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> acionará normalmente apenas para mensagens informativas e de aviso que são enviadas do servidor. No entanto, quando ocorre um erro real, a execução do método **ExecuteNonQuery** ou **ExecuteReader** que iniciou a operação do servidor é interrompida e uma exceção é gerada.  
  
 Se você quiser continuar a processar o restante das instruções em um comando independentemente de qualquer erro gerado pelo servidor, defina a propriedade <xref:System.Data.SqlClient.SqlConnection.FireInfoMessageEventOnUserErrors%2A> do <xref:System.Data.SqlClient.SqlConnection> como `true`. Isso faz a conexão acionar o evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> para erros em vez de gerar uma exceção e interromper o processamento. O aplicativo cliente pode, em seguida, manipular esse evento e responder às condições de erro.  
  
> [!NOTE]
> Um erro com um nível de severidade de 17 ou acima disso faz o servidor parar de processar o comando e deve ser tratado como uma exceção. Nesse caso, uma exceção é gerada independentemente de como o erro é tratado no evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage>.  
  
## <a name="working-with-the-statechange-event"></a>Trabalhando com o evento StateChange  

 O evento **StateChange** ocorre quando o estado de um objeto **Connection** é alterado. O evento **StateChange** recebe <xref:System.Data.StateChangeEventArgs>, que permite determinar a alteração no estado de **Connection** usando as propriedades **OriginalState** e **CurrentState**. A propriedade **OriginalState** é uma enumeração <xref:System.Data.ConnectionState> que indica o estado de **Connection** antes da alteração. **CurrentState** é uma enumeração <xref:System.Data.ConnectionState> que indica o estado de **Connection** após a alteração.  
  
 O exemplo de código a seguir usa o evento **StateChange** para gravar uma mensagem para o console quando o estado de **Connection** muda.  
  
```vb  
' Assumes connection represents a SqlConnection object.  
  AddHandler connection.StateChange, _  
    New StateChangeEventHandler(AddressOf OnStateChange)  
  
Protected Shared Sub OnStateChange( _  
  sender As Object, args As StateChangeEventArgs)  
  
  Console.WriteLine( _  
  "The current Connection state has changed from {0} to {1}.", _  
  args.OriginalState, args.CurrentState)  
End Sub  
```  
  
```csharp  
// Assumes connection represents a SqlConnection object.  
  connection.StateChange  += new StateChangeEventHandler(OnStateChange);  
  
protected static void OnStateChange(object sender,
  StateChangeEventArgs args)  
{  
  Console.WriteLine(  
    "The current Connection state has changed from {0} to {1}.",  
      args.OriginalState, args.CurrentState);  
}  
```  
  
## <a name="see-also"></a>Confira também

- [Conectando a uma Fonte de Dados](connecting-to-a-data-source.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
