---
description: 'Saiba mais sobre: rastreamento de dados em ADO.NET'
title: Rastreamento de dados
ms.date: 03/30/2017
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
ms.openlocfilehash: 7fc4407e76ea34bacc97177d6342730a8263b5c9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663736"
---
# <a name="data-tracing-in-adonet"></a>Rastreamento de dados no ADO.NET

O ADO.NET apresenta a funcionalidade de rastreamento de dados interna com suporte dos provedores de dados .NET para SQL Server, Oracle, OLE DB e ODBC, bem como o ADO.NET <xref:System.Data.DataSet> e os protocolos de rede SQL Server.

O rastreamento de chamadas à API de acesso a dados pode ajudar a diagnosticar os seguintes problemas:

- Incompatibilidade de esquema entre o programa cliente e o banco de dados.

- Problemas de biblioteca de rede ou de indisponibilidade de banco de dados.

- SQL incorreto, seja embutido em código ou gerado por um aplicativo.

- Lógica de programação incorreta.

- Problemas resultantes da interação entre vários componentes do ADO.NET ou entre ADO.NET e seus próprios componentes.

Para dar suporte a diferentes tecnologias de rastreamento, o rastreamento é extensível. Portanto, um desenvolvedor pode rastrear um problema em qualquer nível da pilha de aplicativos. Embora o rastreamento não seja um recurso ADO.NET, os provedores da Microsoft aproveitam as APIs generalizadas de rastreamento e instrumentação.

Para obter mais informações sobre como configurar e configurar o rastreamento gerenciado no ADO.NET, consulte [rastreamento de acesso a dados](/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10)).

## <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Acessar informações de diagnóstico nos logs de eventos estendidos

No .NET Framework Provedor de Dados para SQL Server, o rastreamento de acesso a dados ([rastreamento de acesso a dados](/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10))) foi atualizado para facilitar a correlação de eventos de cliente com informações de diagnóstico, como falhas de conexão, do buffer de anéis de conectividade do servidor e das informações de desempenho do aplicativo no log de eventos estendidos. Para obter mais informações sobre como ler o log de eventos estendidos, consulte [View Event Session Data](/previous-versions/sql/sql-server-2012/hh710068(v=sql.110)).

Para operações de conexão, o ADO.NET enviará uma ID de conexão de cliente. Se houver falha na conexão, você poderá acessar o buffer de anéis de conectividade ([Solução de problemas de conectividade no SQL Server 2008 com o buffer de anéis de conectividade](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer)), localizar o campo `ClientConnectionID` e obter informações de diagnóstico sobre a falha na conexão. As IDs de conexão de cliente estarão registradas no buffer de anéis se um erro ocorrer. (Se uma conexão falhar antes de enviar o pacote anterior ao logon, uma ID conexão de cliente não será gerada.) A ID de conexão de cliente é um GUID de 16 bytes. Você também poderá encontrar a ID de conexão do cliente na saída de destino dos eventos estendidos se a ação `client_connection_id` for adicionada aos eventos em uma sessão de eventos estendidos. Você pode habilitar o rastreamento de acesso a dados e executar novamente o comando de conexão, além de observar o campo `ClientConnectionID` no rastreamento de acesso a dados, caso precise obter assistência adicional com o diagnóstico de driver do cliente.

Você pode obter a ID de conexão do cliente de modo programático usando a propriedade `SqlConnection.ClientConnectionID`.

O `ClientConnectionID` está disponível para um <xref:System.Data.SqlClient.SqlConnection> objeto que estabelece com êxito uma conexão. Se uma tentativa de conexão falhar, a `ClientConnectionID` poderá estar disponível por meio de `SqlException.ToString`.

O ADO.NET também envia uma ID de atividade específica do thread. A ID de atividade é capturada nas sessões de eventos estendidas se as sessões são iniciadas com a opção de TRACK_CAUSALITY habilitada. Para problemas de desempenho com uma conexão ativa, você poderá obter a ID de atividade do rastreamento de acesso a dados do cliente (campo `ActivityID`) e, em seguida, localizar a ID de atividade nas saídas dos eventos estendidos. A ID de atividade nos eventos estendidos é um GUID de 16 bytes (não é o mesmo que o GUID da ID de conexão do cliente) com um número sequencial de quatro bytes. O número de sequência representa a ordem de uma solicitação dentro de um thread e indica a ordenação relativa de lote e as instruções RPC para o thread. No momento, a `ActivityID` é enviada opcionalmente para instruções em lote do SQL e solicitações do RPC quando o rastreamento de acesso a dados está habilitado e o 18º bit na palavra de configuração de rastreamento de acesso a dados está ativado (ON).

Veja a seguir um exemplo que usa o Transact-SQL para iniciar uma sessão de eventos estendidos que será armazenada em um buffer de anéis e registrará a ID de atividade enviada de um cliente em operações RPC e em lote.

```sql
create event session MySession on server
add event connectivity_ring_buffer_recorded,
add event sql_statement_starting (action (client_connection_id)),
add event sql_statement_completed (action (client_connection_id)),
add event rpc_starting (action (client_connection_id)),
add event rpc_completed (action (client_connection_id))
add target ring_buffer with (track_causality=on)
```

## <a name="see-also"></a>Consulte também

- [Rastreamento de rede no .NET Framework](../../network-programming/network-tracing.md)
- [Como rastrear e instrumentar aplicativos](../../debug-trace-profile/tracing-and-instrumenting-applications.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
