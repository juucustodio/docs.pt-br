---
description: 'Saiba mais sobre: execução de SqlCommand com um SqlNotificationRequest'
title: Execução de SqlCommand com um SqlNotificationRequest
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.openlocfilehash: d3e82022794aa67d4bd20223cac852097f2be9dc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767044"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>Execução de SqlCommand com um SqlNotificationRequest

Um <xref:System.Data.SqlClient.SqlCommand> pode ser configurado para gerar uma notificação quando os dados forem alterados após terem sido obtidos do servidor. Além disso, o conjunto de resultados seria diferente caso a consulta seja executada novamente. Isso é útil para cenários em que você deseja usar filas de notificação personalizadas no servidor ou quando não quiser manter objetos dinâmicos.

## <a name="creating-the-notification-request"></a>Criando a solicitação de notificação

É possível usar um objeto <xref:System.Data.Sql.SqlNotificationRequest> para criar a solicitação de notificação associando-o a um objeto `SqlCommand`. Depois que a solicitação for criada, o objeto `SqlNotificationRequest` não será mais necessário. É possível consultar a fila para todas as notificações e responder adequadamente. As notificações podem ocorrer mesmo que o aplicativo seja desligado e reiniciado em seguida.

Quando o comando é executado com a notificação associada, qualquer alteração no conjunto de resultados original dispara o envio de uma mensagem para a fila do SQL Server configurada na solicitação de notificação.

A forma de sondar a fila do SQL Server e interpretar a mensagem é específica para seu aplicativo. O aplicativo é responsável pela sondagem da fila e por reagir com base no conteúdo da mensagem.

> [!NOTE]
> Ao usar as solicitações de notificação do SQL Server com <xref:System.Data.SqlClient.SqlDependency>, crie um nome de fila próprio em vez de usar o nome de serviço padrão.

Não há elementos novos de segurança do lado do cliente para <xref:System.Data.Sql.SqlNotificationRequest>. Esse é basicamente um recurso do servidor. Ele criou privilégios especiais que os usuários devem ter para solicitar uma notificação.

### <a name="example"></a>Exemplo

O fragmento de código a seguir demonstra como criar um <xref:System.Data.Sql.SqlNotificationRequest> e associá-lo a um <xref:System.Data.SqlClient.SqlCommand>.

```vb
' Assume connection is an open SqlConnection.
' Create a new SqlCommand object.
Dim command As New SqlCommand( _
  "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection)

' Create a SqlNotificationRequest object.
Dim notifcationRequest As New SqlNotificationRequest()
notificationRequest.id = "NotificationID"
notificationRequest.Service = "mySSBQueue"

' Associate the notification request with the command.
command.Notification = notificationRequest
' Execute the command.
command.ExecuteReader()
' Process the DataReader.
' You can use Transact-SQL syntax to periodically poll the
' SQL Server queue to see if you have a new message.
```

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="see-also"></a>Consulte também

- [Notificações de consulta no SQL Server](query-notifications-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
