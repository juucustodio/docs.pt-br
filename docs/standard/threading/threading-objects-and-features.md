---
description: 'Saiba mais sobre: objetos e recursos de Threading'
title: Objetos e recursos de threading
ms.date: 10/01/2018
helpviewer_keywords:
- threading [.NET], features
- managed threading
ms.assetid: 239b2e8d-581b-4ca3-992b-0e8525b9321c
ms.openlocfilehash: 7e8167c42780ccc70c37a10bbb3a65483efabb24
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675410"
---
# <a name="threading-objects-and-features"></a>Objetos e recursos de threading

Juntamente com a classe <xref:System.Threading.Thread?displayProperty=nameWithType>, o .NET fornece várias classes que ajudam você a desenvolver aplicativos multithread. Os artigos a seguir fornecem uma visão geral dessas classes:

|Title|Descrição|  
|-----------|-----------------|  
|[O pool de threads gerenciados](the-managed-thread-pool.md)|Descreve a classe <xref:System.Threading.ThreadPool?displayProperty=nameWithType>, que fornece um pool de threads de trabalho que são gerenciados pelo .NET.|  
|[Temporizadores](timers.md)|Descreve os temporizadores do .NET que podem ser usados em um ambiente multi-threaded.|
|[Visão geral dos primitivos de sincronização](overview-of-synchronization-primitives.md)|Descreve os tipos que podem ser usados para sincronizar o acesso a um recurso compartilhado ou uma interação de thread de controle.|
|[EventWaitHandle](eventwaithandle.md)|Descreve a classe <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType>, que representa um evento de sincronização de thread.|
|[CountdownEvent](countdownevent.md)|Descreve a classe <xref:System.Threading.CountdownEvent?displayProperty=nameWithType>, que representa um evento de sincronização de thread que é definido quando sua contagem é zero.|
|[Mutexes](mutexes.md)|Descreve a classe <xref:System.Threading.Mutex?displayProperty=nameWithType>, que permite acesso exclusivo a um recurso compartilhado.|
|[Semaphore e SemaphoreSlim](semaphore-and-semaphoreslim.md)|Descreve a classe <xref:System.Threading.Semaphore?displayProperty=nameWithType>, que limita o número de threads que podem acessar um recurso compartilhado ou um pool de recursos simultaneamente.|
|[Barreira](barrier.md)|Descreve a classe <xref:System.Threading.Barrier?displayProperty=nameWithType> que implementa o padrão de barreira para a coordenação de threads em operações em fases.|
|[SpinLock](spinlock.md)|Descreve a estrutura <xref:System.Threading.SpinLock?displayProperty=nameWithType>, que é uma alternativa leve à classe <xref:System.Threading.Monitor?displayProperty=nameWithType> para certos cenários de bloqueio de nível baixo.|
|[SpinWait](spinwait.md)|Descreve a estrutura de <xref:System.Threading.SpinWait?displayProperty=nameWithType>, que fornece suporte para espera baseada em rotação.|

## <a name="see-also"></a>Consulte também

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.WaitHandle?displayProperty=nameWithType>
- <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- [Usando threads e threading](using-threads-and-threading.md)
- [E/s de arquivo assíncrono](../io/asynchronous-file-i-o.md)
- [Programação paralela](../parallel-programming/index.md)
- [Biblioteca de tarefas paralelas (TPL)](../parallel-programming/task-parallel-library-tpl.md)
