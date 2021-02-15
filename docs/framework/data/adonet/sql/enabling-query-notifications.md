---
description: 'Saiba mais sobre: habilitando notificações de consulta'
title: Habilitando notificações de consulta
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.openlocfilehash: e0ff405477a9faa141ce81c5ac8ba2d1ace95501
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663333"
---
# <a name="enabling-query-notifications"></a>Habilitando notificações de consulta

Os aplicativos que consomem notificações de consulta têm um conjunto comum de requisitos. Sua fonte de dados deve ser configurada corretamente para dar suporte a notificações de consulta SQL e o usuário deve ter as permissões corretas de cliente e servidor.  
  
 Para usar as notificações de consulta, você deve:  
  
- Habilitar as notificações de consulta para seu banco de dados.  
  
- Verificar se a ID de usuário usada para se conectar ao banco de dados tem as permissões necessárias.  
  
- Usar um objeto <xref:System.Data.SqlClient.SqlCommand> para executar uma instrução SELECT válida com um objeto de notificação associado – seja <xref:System.Data.SqlClient.SqlDependency> ou <xref:System.Data.Sql.SqlNotificationRequest>.  
  
- Fornecer o código para processar a notificação se os dados que estão sendo monitorados forem alterados.  
  
## <a name="query-notifications-requirements"></a>Requisitos de notificações de consulta  

 As notificações de consulta são compatíveis apenas com instruções SELECT que atendem a uma lista de requisitos específicos. A tabela a seguir fornece links para a documentação do Service Broker e das notificações de consulta nos Manuais Online do SQL Server.  
  
 **Documentação do SQL Server**  
  
- [Criando uma consulta para notificação](/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Considerações de segurança para Service Broker](/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [Segurança e proteção (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Considerações de segurança para serviços de notificação](/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [Permissões de notificação de consulta](/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Considerações internacionais para Service Broker](/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [Considerações sobre design de solução (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker Developer InfoCenter](/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [Guia do desenvolvedor (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>Habilitando notificações de consulta para executar código de exemplo  

 Para habilitar o Service Broker no banco de dados **AdventureWorks** usando o SQL Server Management Studio, execute a seguinte instrução Transact-SQL:  
  
 `ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
 Para que os exemplos de notificação de consulta sejam executados corretamente, as instruções Transact-SQL a seguir devem ser executadas no servidor de banco de dados.  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>Permissões de notificações de consulta  

 Os usuários que executam comandos solicitando notificação devem ter a permissão de banco de dados SUBSCRIBE QUERY NOTIFICATIONS no servidor.  
  
 O código do lado do cliente que é executado em uma situação de confiança parcial requer o <xref:System.Data.SqlClient.SqlClientPermission>.  
  
 O código a seguir cria um objeto <xref:System.Data.SqlClient.SqlClientPermission>, configurando o <xref:System.Security.Permissions.PermissionState> como <xref:System.Security.Permissions.PermissionState.Unrestricted>. O <xref:System.Security.CodeAccessPermission.Demand%2A> forçará um <xref:System.Security.SecurityException> em tempo de execução se todos os chamadores mais acima na pilha de chamadas não tiverem recebido a permissão.  
  
 [!code-csharp[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/CS/source.cs#1)]
 [!code-vb[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/VB/source.vb#1)]  
  
## <a name="choosing-a-notification-object"></a>Escolhendo um objeto de notificação  

 A API de notificações de consulta fornece dois objetos para processar notificações: <xref:System.Data.SqlClient.SqlDependency> e <xref:System.Data.Sql.SqlNotificationRequest>. Em geral, a maioria dos aplicativos que não sejam ASP.NET devem usar o objeto <xref:System.Data.SqlClient.SqlDependency>. Os aplicativos ASP.NET devem usar o <xref:System.Web.Caching.SqlCacheDependency> de nível mais alto, que envolve <xref:System.Data.SqlClient.SqlDependency> e fornece uma estrutura para administrar os objetos de notificação e cache.  
  
### <a name="using-sqldependency"></a>Como usar SqlDependency  

 Para usar <xref:System.Data.SqlClient.SqlDependency>, o Service Broker deverá ser habilitado para o Banco de Dados do SQL Server usado e os usuários devem ter permissões para receber notificações. Os objetos do Service Broker, como a fila de notificação, são predefinidos.  
  
 Além disso, o <xref:System.Data.SqlClient.SqlDependency> inicia automaticamente um thread de trabalho para processar as notificações à medida que elas são postadas na fila. Ele também analisa a mensagem do Service Broker, expondo as informações como dados de argumento do evento. O <xref:System.Data.SqlClient.SqlDependency> deve ser inicializado chamando o método `Start` para estabelecer uma dependência com o banco de dados. Esse é um método estático que precisa ser chamado apenas uma vez durante a inicialização do aplicativo para cada conexão de banco de dados necessária. O método `Stop` deve ser chamado na terminação do aplicativo para cada conexão de dependência que foi feita.  
  
### <a name="using-sqlnotificationrequest"></a>Como usar SqlNotificationRequest  

 Por outro lado, o <xref:System.Data.Sql.SqlNotificationRequest> exige que você implemente toda a infraestrutura de escuta por conta própria. Além disso, todos os objetos do Service Broker de suporte, como os tipos de fila, serviço e mensagem compatíveis com a fila, devem ser definidos. Essa abordagem manual será útil se o aplicativo exigir mensagens de notificação especiais ou comportamentos de notificação ou se o aplicativo fizer parte de um aplicativo de Service Broker maior.  
  
## <a name="see-also"></a>Consulte também

- [Notificações de consulta no SQL Server](query-notifications-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
