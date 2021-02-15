---
title: EventCounters bem conhecido no .NET
description: Examine o EventCounters publicado pelo tempo de execução e pelas bibliotecas do .NET.
ms.topic: reference
ms.date: 12/17/2020
ms.openlocfilehash: 8bd14c7caf004cefe73d5b0676b9fa3280840442
ms.sourcegitcommit: c3093e9d106d8ca87cc86eef1f2ae4ecfb392118
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2020
ms.locfileid: "97737288"
---
# <a name="well-known-eventcounters-in-net"></a>EventCounters bem conhecido no .NET

O tempo de execução e as bibliotecas do .NET implementam e publicam várias [`EventCounter`](./event-counters.md) que podem ser usadas para identificar e diagnosticar vários problemas de desempenho. Este documento é uma referência nos provedores que podem ser usados para monitorá-los `EventCounters` e suas descrições.

## <a name="systemruntime-counters"></a>Contadores System. Runtime

Os contadores a seguir são publicados como parte do tempo de execução do .NET (CoreCLR) e são mantidos no [`RuntimeEventSource.cs`](https://github.com/dotnet/coreclr/blob/master/src/System.Private.CoreLib/src/System/Diagnostics/Eventing/RuntimeEventSource.cs) .

| Contador | Descrição |
|--|--|
| :::no-loc text="% Time in GC since last GC"::: (`time-in-gc`) | A porcentagem de tempo no GC desde o último GC |
| :::no-loc text="Allocation Rate"::: (`alloc-rate`) | O número de bytes alocados por intervalo de atualização |
| :::no-loc text="CPU Usage"::: (`cpu-usage`) | A porcentagem do uso da CPU do processo em relação a todos os recursos de CPU do sistema |
| :::no-loc text="Exception Count"::: (`exception-count`) | O número de exceções que ocorreram |
| :::no-loc text="GC Heap Size"::: (`gc-heap-size`) | O número de bytes considerados alocados com base em <xref:System.GC.GetTotalMemory(System.Boolean)?displayProperty=nameWithType> |
| :::no-loc text="Gen 0 GC Count"::: (`gen-0-gc-count`) | O número de vezes que GC ocorreu para Gen 0 por intervalo de atualização |
| :::no-loc text="Gen 0 Size"::: (`gen-0-size`) | O número de bytes para Gen 0 GC |
| :::no-loc text="Gen 1 GC Count"::: (`gen-1-gc-count`) | O número de vezes que GC ocorreu para Gen 1 por intervalo de atualização |
| :::no-loc text="Gen 1 Size"::: (`gen-1-size`) | O número de bytes para Gen 1 GC |
| :::no-loc text="Gen 2 GC Count"::: (`gen-2-gc-count`) | O número de vezes que GC ocorreu para Gen 2 por intervalo de atualização |
| :::no-loc text="Gen 2 Size"::: (`gen-2-size`) | O número de bytes para Gen 2 GC |
| :::no-loc text="LOH Size"::: (`loh-size`) | O número de bytes para o heap de objeto grande |
| :::no-loc text="POH Size"::: (`poh-size`) | O número de bytes para o heap de objeto fixado (disponível no .NET 5 e versões posteriores) |
| :::no-loc text="GC Fragmentation"::: (`gc-fragmentation`) | A fragmentação do heap de GC (disponível no .NET 5 e versões posteriores) |
| :::no-loc text="Monitor Lock Contention Count"::: (`monitor-lock-contention-count`) | O número de vezes que houve contenção ao tentar usar o bloqueio do monitor, com base em <xref:System.Threading.Monitor.LockContentionCount?displayProperty=nameWithType> |
| :::no-loc text="Number of Active Timers"::: (`active-timer-count`) | O número de <xref:System.Threading.Timer> instâncias atualmente ativas, com base em <xref:System.Threading.Timer.ActiveCount?displayProperty=nameWithType> |
| :::no-loc text="Number of Assemblies Loaded"::: (`assembly-count`) | O número de <xref:System.Reflection.Assembly> instâncias carregadas em um processo em um ponto no tempo |
| :::no-loc text="ThreadPool Completed Work Item Count"::: (`threadpool-completed-items-count`) | O número de itens de trabalho que foram processados até o momento no <xref:System.Threading.ThreadPool> |
| :::no-loc text="ThreadPool Queue Length"::: (`threadpool-queue-length`) | O número de itens de trabalho que estão enfileirados no momento para serem processados no <xref:System.Threading.ThreadPool> |
| :::no-loc text="ThreadPool Thread Count"::: (`threadpool-thread-count`) | O número de threads do pool de threads que existem atualmente no <xref:System.Threading.ThreadPool> , com base em <xref:System.Threading.ThreadPool.ThreadCount?displayProperty=nameWithType> |
| :::no-loc text="Working Set"::: (`working-set`) | A quantidade de memória física mapeada para o contexto do processo em uma base pontual em <xref:System.Environment.WorkingSet?displayProperty=nameWithType> |
| :::no-loc text="IL Bytes Jitted"::: (`il-bytes-jitted`) | O tamanho total do ILs que são compilados em JIT, em bytes (disponíveis no .NET 5 e em versões posteriores) |
| :::no-loc text="Method Jitted Count"::: (`method-jitted-count`) | O número de métodos compilados por JIT (disponíveis no .NET 5 e versões posteriores) |

## <a name="microsoftaspnetcorehosting-counters"></a>Contadores "Microsoft. AspNetCore. Hosting"

Os contadores a seguir são publicados como parte do [ASP.NET Core](/aspnet/core) e são mantidos no [`HostingEventSource.cs`](https://github.com/dotnet/aspnetcore/blob/master/src/Hosting/Hosting/src/Internal/HostingEventSource.cs) .

| Contador | Descrição |
|--|--|
| :::no-loc text="Current Requests"::: (`current-requests`) | O número total de solicitações que foram iniciadas, mas ainda não foram interrompidas |
| :::no-loc text="Failed Requests"::: (`failed-requests`) | O número total de solicitações com falha ocorridas durante a vida útil do aplicativo |
| :::no-loc text="Request Rate"::: (`requests-per-second`) | O número de solicitações que ocorrem por intervalo de atualização |
| :::no-loc text="Total Requests"::: (`total-requests`) | O número total de solicitações que ocorreram durante a vida útil do aplicativo |

## <a name="microsoftaspnetcorehttpconnections-counters"></a>Contadores "Microsoft. AspNetCore. http. Connections"

Os contadores a seguir são publicados como parte do [ASP.NET Core signalr](/aspnet/core/signalr/introduction) e são mantidos no [`HttpConnectionsEventSource.cs`](https://github.com/dotnet/aspnetcore/blob/master/src/SignalR/common/Http.Connections/src/Internal/HttpConnectionsEventSource.cs) .

| Contador | Descrição |
|--|--|
| :::no-loc text="Average Connection Duration"::: (`connections-duration`) | A duração média de uma conexão em milissegundos |
| :::no-loc text="Current Connections"::: (`current-connections`) | O número de conexões ativas que foram iniciadas, mas ainda não foram interrompidas |
| :::no-loc text="Total Connections Started"::: (`connections-started`) | O número total de conexões que foram iniciadas |
| :::no-loc text="Total Connections Stopped"::: (`connections-stopped`) | O número total de conexões que foram interrompidas |
| :::no-loc text="Total Connections Timed Out"::: (`connections-timed-out`) | O número total de conexões que atingiram o tempo limite |

## <a name="microsoft-aspnetcore-server-kestrel-counters"></a>Contadores "Microsoft-AspNetCore-Server-Kestrel"

Os contadores a seguir são publicados como parte do [servidor web ASP.NET Core Kestrel](/aspnet/core/fundamentals/servers/kestrel) e são mantidos no [`KestrelEventSource.cs`](https://github.com/dotnet/aspnetcore/blob/master/src/Servers/Kestrel/Core/src/Internal/Infrastructure/KestrelEventSource.cs) .

| Contador | Descrição |
|--|--|
| :::no-loc text="Connection Queue Length"::: (`connection-queue-length`) | O comprimento atual da fila de conexão |
| :::no-loc text="Connection Rate"::: (`connections-per-second`) | O número de conexões por intervalo de atualização para o servidor Web |
| :::no-loc text="Current Connections"::: (`current-connections`) | O número atual de conexões ativas com o servidor Web |
| :::no-loc text="Current TLS Handshakes"::: (`current-tls-handshakes`) | O número atual de Handshakes TLS |
| :::no-loc text="Current Upgraded Requests (WebSockets)"::: (`current-upgraded-requests`) | O número atual de solicitações atualizadas (WebSockets) |
| :::no-loc text="Failed TLS Handshakes"::: (`failed-tls-handshakes`) | O número total de Handshakes de TLS com falha |
| :::no-loc text="Request Queue Length"::: (`request-queue-length`) | O comprimento atual da fila de solicitações |
| :::no-loc text="TLS Handshake Rate"::: (`tls-handshakes-per-second`) | O número de Handshakes TLS por intervalo de atualização |
| :::no-loc text="Total Connections"::: (`total-connections`) | O número total de conexões com o servidor Web |
| :::no-loc text="Total TLS Handshakes"::: (`total-tls-handshakes`) | O número total de Handshakes TLS com o servidor Web |

## <a name="systemnethttp-counters"></a>Contadores de "System .net. http"

Os contadores a seguir são publicados pela pilha HTTP.  Esses contadores estão disponíveis somente no .NET 5 e em versões posteriores.

| Contador | Descrição |
|--|--|
| :::no-loc text="Requests Started"::: (`requests-started`) | O número de solicitações iniciadas desde o início do processo |
| :::no-loc text="Requests Started Rate"::: (`requests-started-rate`) | O número de solicitações iniciadas por intervalo de atualização |
| :::no-loc text="Requests Failed"::: (`requests-failed`) | O número de solicitações com falha desde o início do processo |
| :::no-loc text="Requests Failed Rate"::: (`requests-failed-rate`) | O número de solicitações com falha por intervalo de atualização |
| :::no-loc text="Current Requests"::: (`current-requests`) | Número atual de solicitações HTTP ativas que foram iniciadas, mas ainda não concluídas ou com falha |
| :::no-loc text="Current HTTP 1.1 Connections"::: (`http11-connections-current-total`) | O número atual de conexões HTTP 1,1 que foram iniciadas, mas que ainda não foram concluídas ou falharam |
| :::no-loc text="Current HTTP 2.0 Connections"::: (`http20-connections-current-total`) | O número atual de conexões HTTP 2,0 que foram iniciadas, mas que ainda não foram concluídas ou falharam |
| :::no-loc text="HTTP 1.1 Requests Queue Duration"::: (`http11-requests-queue-duration`) | A duração média da hora em que as solicitações HTTP 1,1 gastam na fila de solicitações |
| :::no-loc text="HTTP 2.0 Requests Queue Duration"::: (`http20-requests-queue-duration`) | A duração média da hora em que as solicitações HTTP 2,0 gastam na fila de solicitações |

## <a name="systemnetnameresolution-counters"></a>Contadores de "System .net. NameResolution"

Os contadores a seguir acompanham as métricas relacionadas a pesquisas de DNS. Esses contadores estão disponíveis somente no .NET 5 e em versões posteriores.

| Contador | Descrição |
|--|--|
| :::no-loc text="DNS Lookups Requested"::: (`dns-lookups-requested`) | O número de pesquisas de DNS solicitadas desde o início do processo |
| :::no-loc text="Average DNS Lookup Duration"::: (`dns-lookups-duration`) | O tempo médio necessário para uma pesquisa de DNS |

## <a name="systemnetsecurity-counters"></a>Contadores de "System .net. Security"

Os contadores a seguir acompanham as métricas relacionadas ao protocolo de segurança da camada de transporte.  Esses contadores estão disponíveis somente no .NET 5 e em versões posteriores.

| Contador | Descrição |
|--|--|
| :::no-loc text="TLS handshakes completed"::: (`tls-handshake-rate`) | O número de Handshakes TLS concluídos por intervalo de atualização |
| :::no-loc text="Total TLS handshakes completed"::: (`total-tls-handshakes`) | O número total de Handshakes TLS concluídos desde o início do processo |
| :::no-loc text="Current TLS handshakes"::: (`current-tls-handshakes`) | O número atual de Handshakes TLS que foram iniciados, mas que ainda não foram concluídos |
| :::no-loc text="Total TLS handshakes failed"::: (`failed-tls-handshakes`) | O número total de Handshakes de TLS com falha desde o início do processo |
| :::no-loc text="All TLS Sessions Active"::: (`all-tls-sessions-open`) | O número de sessões de TLS ativas de qualquer versão |
| :::no-loc text="TLS 1.0 Sessions Active"::: (`tls10-sessions-open`) | O número de sessões ativas do TLS 1,0 |
| :::no-loc text="TLS 1.1 Sessions Active"::: (`tls11-sessions-open`) | O número de sessões ativas do TLS 1,1 |
| :::no-loc text="TLS 1.2 Sessions Active"::: (`tls12-sessions-open`) | O número de sessões ativas do TLS 1,2 |
| :::no-loc text="TLS 1.3 Sessions Active"::: (`tls13-sessions-open`) | O número de sessões ativas do TLS 1,3 |
| :::no-loc text="TLS Handshake Duration"::: (`all-tls-handshake-duration`) | A duração média de todos os Handshakes de TLS |
| :::no-loc text="TLS 1.0 Handshake Duration"::: (`tls10-handshake-duration`) | A duração média dos Handshakes TLS 1,0 |
| :::no-loc text="TLS 1.1 Handshake Duration"::: (`tls11-handshake-duration`) | A duração média dos Handshakes TLS 1,1 |
| :::no-loc text="TLS 1.2 Handshake Duration"::: (`tls12-handshake-duration`) | A duração média dos Handshakes TLS 1,2 |
| :::no-loc text="TLS 1.3 Handshake Duration"::: (`tls13-handshake-duration`) | A duração média dos Handshakes TLS 1,3 |

## <a name="systemnetsockets-counters-available-on-net-5-and-later-versions"></a>Contadores de "System .net. Sockets" (disponíveis no .NET 5 e versões posteriores)

Os contadores a seguir acompanham as métricas relacionadas ao <xref:System.Net.Sockets.Socket> .

| Contador | Descrição |
|--|--|
| :::no-loc text="Outgoing Connections Established"::: (`outgoing-connections-established`) | O número total de conexões de saída estabelecidas desde o início do processo |
| :::no-loc text="Incoming Connections Established"::: (`incoming-connections-established`) | O número total de conexões de entrada estabelecidas desde o início do processo |
| :::no-loc text="Bytes Received"::: (`bytes-received`) | O número total de bytes recebidos desde o início do processo |
| :::no-loc text="Bytes Sent"::: (`bytes-sent`) | O número total de bytes enviados desde o início do processo |
| :::no-loc text="Datagrams Received"::: (`datagrams-received`) | O número total de datagramas recebidos desde o início do processo |
| :::no-loc text="Datagrams Sent"::: (`datagrams-sent`) | O número total de datagrams enviados desde o início do processo |
