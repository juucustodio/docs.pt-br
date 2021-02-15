---
title: Visão geral dos primitivos de sincronização
description: Saiba mais sobre os primitivos de sincronização de thread do .NET usados para sincronizar o acesso a uma interação de thread de controle ou recurso compartilhado
ms.date: 10/01/2018
helpviewer_keywords:
- synchronization, threads
- threading [.NET],synchronizing threads
- managed threading
ms.assetid: b782bcb8-da6a-4c6a-805f-2eb46d504309
ms.openlocfilehash: 9dfaaa6050cc6e9a6b86f991aa6d2ce2a815959a
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94819650"
---
# <a name="overview-of-synchronization-primitives"></a>Visão geral dos primitivos de sincronização

O .NET fornece uma variedade de tipos que você pode usar para sincronizar o acesso a um recurso compartilhado ou coordenar a interação de thread.

> [!IMPORTANT]
> Use a mesma instância de primitivos de sincronização para proteger o acesso de um recurso compartilhado. Se usar instâncias primitivas de sincronização diferentes para proteger o mesmo recurso, você evitará a proteção fornecida por um primitivo de sincronização.

## <a name="waithandle-class-and-lightweight-synchronization-types"></a>Tipos de sincronização leve e a classe WaitHandle

Vários primitivos de sincronização .NET derivam da classe <xref:System.Threading.WaitHandle?displayProperty=nameWithType>, que encapsula um identificador de sincronização do sistema operacional nativo e usa um mecanismo de sinalização de interação de thread. Essas classes incluem:

- <xref:System.Threading.Mutex?displayProperty=nameWithType>, que concede acesso exclusivo a um recurso compartilhado. O estado de um mutex será sinalizado se nenhum thread for seu proprietário.
- <xref:System.Threading.Semaphore?displayProperty=nameWithType>, que limita o número de threads que podem acessar um recurso compartilhado ou um pool de recursos simultaneamente. O estado de um semáforo é definido como sinalizado quando a contagem é maior que zero e não sinalizado quando a contagem é zero.
- <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType>, que representa um evento de sincronização de thread e pode estar em um estado sinalizado ou não sinalizado.
- <xref:System.Threading.AutoResetEvent?displayProperty=nameWithType>, que é derivado de <xref:System.Threading.EventWaitHandle> e, quando sinalizado, é redefinido automaticamente para um estado não sinalizado após o lançamento de um único thread em espera.
- <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType>, que é derivado de <xref:System.Threading.EventWaitHandle> e, quando sinalizado, permanece no estado sinalizado até que o método <xref:System.Threading.EventWaitHandle.Reset%2A> seja chamado.

Em .NET Framework, como <xref:System.Threading.WaitHandle> deriva de <xref:System.MarshalByRefObject?displayProperty=nameWithType> , esses tipos podem ser usados para sincronizar as atividades de threads entre limites de domínio do aplicativo.

No .NET Framework, no .NET Core e no .NET 5 +, alguns desses tipos podem representar identificadores de sincronização do sistema nomeados, que são visíveis em todo o sistema operacional e podem ser usados para a sincronização entre processos:

- <xref:System.Threading.Mutex>
- <xref:System.Threading.Semaphore> (no Windows)
- <xref:System.Threading.EventWaitHandle> (no Windows)

Para obter mais informações, veja a referência de API <xref:System.Threading.WaitHandle>.

Tipos de sincronização leve não dependem de identificadores do sistema operacional subjacente e normalmente fornecem um melhor desempenho. No entanto, não podem ser usados para a sincronização entre processos. Use esses tipos para sincronização de thread dentro de um aplicativo.

Alguns desses tipos são alternativas aos tipos derivados de <xref:System.Threading.WaitHandle>. Por exemplo, <xref:System.Threading.SemaphoreSlim> é uma alternativa leve para <xref:System.Threading.Semaphore>.

## <a name="synchronization-of-access-to-a-shared-resource"></a>Sincronização de acesso a um recurso compartilhado

O .NET fornece uma variedade de primitivos de sincronização para controlar o acesso a um recurso compartilhado por vários threads.

### <a name="monitor-class"></a>Classe Monitor

A classe <xref:System.Threading.Monitor?displayProperty=nameWithType> concede acesso mutuamente exclusivo em um recurso compartilhado, adquirindo ou liberando um bloqueio no objeto que identifica o recurso. Embora um bloqueio seja mantido, o thread que mantém o bloqueio pode adquiri-lo novamente e liberá-lo. Qualquer outro thread é impedido de adquirir o bloqueio e o método <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> aguardará até que o bloqueio seja liberado. O método <xref:System.Threading.Monitor.Enter%2A> adquire um bloqueio liberado. Você também pode usar o método <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType> para especificar o tempo durante o qual um thread tenta adquirir um bloqueio. Porque a classe <xref:System.Threading.Monitor> tem afinidade de thread, o thread que adquiriu um bloqueio deve liberar o bloqueio chamando o método <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType>.

Você pode coordenar a interação de threads que adquirirem um bloqueio no mesmo objeto usando os métodos <xref:System.Threading.Monitor.Wait%2A?displayProperty=nameWithType>, <xref:System.Threading.Monitor.Pulse%2A?displayProperty=nameWithType> e <xref:System.Threading.Monitor.PulseAll%2A?displayProperty=nameWithType>.

Para obter mais informações, veja a referência de API <xref:System.Threading.Monitor>.

> [!NOTE]
> Use a instrução [lock](../../csharp/language-reference/keywords/lock-statement.md) no C# e a instrução [SyncLock](../../visual-basic/language-reference/statements/synclock-statement.md) no Visual Basic para sincronizar o acesso a um recurso compartilhado, em vez de usar a classe <xref:System.Threading.Monitor> diretamente. Essas instruções são implementadas usando os métodos <xref:System.Threading.Monitor.Enter%2A> e <xref:System.Threading.Monitor.Exit%2A> e um bloco `try…finally` para garantir que o bloqueio adquirido sempre seja liberado.

### <a name="mutex-class"></a>Classe Mutex

A classe <xref:System.Threading.Mutex?displayProperty=nameWithType>, como <xref:System.Threading.Monitor>, concede acesso exclusivo a um recurso compartilhado. Use uma das sobrecargas do método [Mutex.WaitOne](<xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=nameWithType>) para solicitar a propriedade de um mutex. Como <xref:System.Threading.Monitor>, <xref:System.Threading.Mutex> tem afinidade de thread e o thread que adquiriu um mutex deverá liberá-lo chamando o método <xref:System.Threading.Mutex.ReleaseMutex%2A?displayProperty=nameWithType>.

Diferente de <xref:System.Threading.Monitor>, a classe <xref:System.Threading.Mutex> pode ser usada para sincronização entre processos. Para fazer isso, use um mutex nomeado, que fica visível em todo o sistema operacional. Para criar uma instância de mutex nomeada, use um [construtor Mutex](<xref:System.Threading.Mutex.%23ctor%2A>) que especifique um nome. Você também pode chamar o <xref:System.Threading.Mutex.OpenExisting%2A?displayProperty=nameWithType> método para abrir um mutex de sistema nomeado existente.
  
Para obter mais informações, veja o artigo [Mutexes](mutexes.md) e a referência da API <xref:System.Threading.Mutex>.

### <a name="spinlock-structure"></a>Estrutura de SpinLock

A estrutura <xref:System.Threading.SpinLock?displayProperty=nameWithType>, como <xref:System.Threading.Monitor>, concede acesso exclusivo a um recurso compartilhado com base na disponibilidade de um bloqueio. Quando <xref:System.Threading.SpinLock> tenta adquirir um bloqueio que não está disponível, ele aguarda em um loop, verificando repetidamente até o bloqueio ficar disponível.

Para obter mais informações sobre as vantagens e as desvantagens do uso do bloqueio de rotação, veja o artigo [SpinLock](spinlock.md) e a referência da API <xref:System.Threading.SpinLock>.

### <a name="readerwriterlockslim-class"></a>Classe ReaderWriterLockSlim

A classe <xref:System.Threading.ReaderWriterLockSlim?displayProperty=nameWithType> concede acesso exclusivo a um recurso compartilhado para gravação e permite que vários threads acessem o recurso simultaneamente para leitura. Você talvez queira usar <xref:System.Threading.ReaderWriterLockSlim> para sincronizar o acesso a uma estrutura de dados compartilhada que dá suporte a operações de leitura thread-safe, mas requer acesso exclusivo para realizar a operação de gravação. Quando um thread solicita acesso exclusivo (por exemplo, ao chamar o método <xref:System.Threading.ReaderWriterLockSlim.EnterWriteLock%2A?displayProperty=nameWithType>), o leitor subsequente solicita o bloqueio até que todos os leitores e gravadores existentes tenham saído do bloqueio e o gravador tenha entrado e saído do bloqueio.
  
Para obter mais informações, veja a referência de API <xref:System.Threading.ReaderWriterLockSlim>.

### <a name="semaphore-and-semaphoreslim-classes"></a>Classes Semaphore e SemaphoreSlim

As classes <xref:System.Threading.Semaphore?displayProperty=nameWithType> e <xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType> limitam o número de threads que podem acessar um recurso compartilhado ou um pool de recursos simultaneamente. Threads adicionais que solicitam o recurso aguardam até que qualquer thread liberar o semáforo. Como o semáforo não tem afinidade de thread, um thread pode adquirir o semáforo e outro pode liberá-lo.

<xref:System.Threading.SemaphoreSlim> é uma alternativa leve a <xref:System.Threading.Semaphore> e pode ser usado somente para sincronização dentro do limite de um único processo.

No Windows, você pode usar <xref:System.Threading.Semaphore> para a sincronização entre processos. Para fazer isso, crie uma instância <xref:System.Threading.Semaphore> que representa um semáforo de sistema nomeado usando um dos [Construtores de semáforo](<xref:System.Threading.Semaphore.%23ctor%2A>) que especifica um nome ou o método <xref:System.Threading.Semaphore.OpenExisting%2A?displayProperty=nameWithType>. <xref:System.Threading.SemaphoreSlim> não dá suporte a sinais de sistema nomeado.

Para obter mais informações, veja o artigo [Semaphore e SemaphoreSlim](semaphore-and-semaphoreslim.md) e a referência à API <xref:System.Threading.Semaphore> ou <xref:System.Threading.SemaphoreSlim>.

## <a name="thread-interaction-or-signaling"></a>Interação ou sinalização de thread

Interação de thread (ou sinalização do thread) significa que um thread deve aguardar notificação ou um sinal de um ou mais threads para continuar. Por exemplo, se o thread A chamar o método <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> do thread B, o thread A será bloqueado até que o thread B seja concluído. Os primitivos de sincronização descritos na seção anterior fornecem um mecanismo diferente para sinalização: ao liberar um bloqueio, um thread notifica outro thread de que ele pode continuar adquirindo o bloqueio.

Esta seção descreve outras construções de sinalização fornecidas pelo .NET.

### <a name="eventwaithandle-autoresetevent-manualresetevent-and-manualreseteventslim-classes"></a>Classes EventWaitHandle, AutoResetEvent, ManualResetEvent e ManualResetEventSlim

A classe <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> representa um evento de sincronização de thread.

Um evento de sincronização pode estar em um estado não sinalizado ou sinalizado. Quando o estado de um evento não é sinalizado, um thread que chama a sobrecarga <xref:System.Threading.WaitHandle.WaitOne%2A?> do evento é bloqueado até que um evento seja sinalizado. O método <xref:System.Threading.EventWaitHandle.Set%2A?displayProperty=nameWithType> define o estado de um evento como sinalizado.

O comportamento de um <xref:System.Threading.EventWaitHandle> que foi assinalado depende de seu modo de redefinição:

- Um <xref:System.Threading.EventWaitHandle> criado com o sinalizador <xref:System.Threading.EventResetMode.AutoReset?displayProperty=nameWithType> é redefinido automaticamente após liberar um único thread em espera. É como uma roleta que permite que apenas um thread de cada vez seja sinalizado. A classe <xref:System.Threading.AutoResetEvent?displayProperty=nameWithType>, que deriva de <xref:System.Threading.EventWaitHandle>, representa esse comportamento.
- Um <xref:System.Threading.EventWaitHandle> criado com o sinalizador <xref:System.Threading.EventResetMode.ManualReset?displayProperty=nameWithType> permanece sinalizado até que seu método <xref:System.Threading.EventWaitHandle.Reset%2A> seja chamado. É como um portão que é fechado até ser sinalizado e então permanece aberto até que alguém o feche. A classe <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType>, que deriva de <xref:System.Threading.EventWaitHandle>, representa esse comportamento. A classe <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> é uma alternativa leve para <xref:System.Threading.ManualResetEvent>.

No Windows, você pode usar <xref:System.Threading.EventWaitHandle> para a sincronização entre processos. Para fazer isso, crie uma instância <xref:System.Threading.EventWaitHandle> que representa um evento de sincronização do sistema nomeado usando um dos [construtores EventWaitHandle](<xref:System.Threading.EventWaitHandle.%23ctor%2A>) que especificam um nome ou o método <xref:System.Threading.EventWaitHandle.OpenExisting%2A?displayProperty=nameWithType>.

Para obter mais informações, confira o artigo [EventWaitHandle](eventwaithandle.md). Para a referência de API, veja <xref:System.Threading.EventWaitHandle>, <xref:System.Threading.AutoResetEvent>, <xref:System.Threading.ManualResetEvent> e <xref:System.Threading.ManualResetEventSlim>.

### <a name="countdownevent-class"></a>Classe CountdownEvent

A classe <xref:System.Threading.CountdownEvent?displayProperty=nameWithType> representa um evento definido quando a contagem é zero. Embora <xref:System.Threading.CountdownEvent.CurrentCount?displayProperty=nameWithType> seja maior que zero, um thread que chama <xref:System.Threading.CountdownEvent.Wait%2A?displayProperty=nameWithType> é bloqueado. Chame <xref:System.Threading.CountdownEvent.Signal%2A?displayProperty=nameWithType> para diminuir a contagem de um evento.

Em contraste com <xref:System.Threading.ManualResetEvent> ou <xref:System.Threading.ManualResetEventSlim>, que você pode usar para desbloquear vários threads com um sinal de um thread, você pode usar <xref:System.Threading.CountdownEvent> para desbloquear um ou mais threads com sinais de vários threads.

Para obter mais informações, veja o artigo [CountdownEvent](countdownevent.md) e a referência à API <xref:System.Threading.CountdownEvent>.

### <a name="barrier-class"></a>Classe de barreira

A classe <xref:System.Threading.Barrier?displayProperty=nameWithType> representa uma barreira de execução do thread. Um thread que chama o método <xref:System.Threading.Barrier.SignalAndWait%2A?displayProperty=nameWithType> sinaliza que atingiu a barreira e aguarda até que outros threads participantes atinjam a barreira. Quando todos os threads participantes atingem a barreira, eles prosseguem e a barreira é redefinida e pode ser usada novamente.

Você pode usar <xref:System.Threading.Barrier> quando um ou mais threads exigirem os resultados de outros threads antes de prosseguir para a próxima fase de cálculo.

Para obter mais informações, veja o artigo [Barreira](barrier.md) e a referência da API <xref:System.Threading.Barrier>.

## <a name="interlocked-class"></a>Classe Interlocked

A classe <xref:System.Threading.Interlocked?displayProperty=nameWithType> fornece métodos estáticos que executam operações atômicas simples em uma variável. Essas operações atômicas incluem adição, incremento e decremento, troca e troca condicional que depende de uma comparação e operação de leitura de um valor inteiro de 64 bits.

Para obter mais informações, veja a referência de API <xref:System.Threading.Interlocked>.

## <a name="spinwait-structure"></a>Estrutura SpinWait

A estrutura <xref:System.Threading.SpinWait?displayProperty=nameWithType> oferece suporte para espera baseada em rotação. Você pode usá-la quando um thread tiver de esperar pela sinalização de um evento ou por uma condição específica. No entanto, quando o tempo de espera real for menor do que o tempo necessário, use um identificador de espera ou bloqueie o thread. Usando o <xref:System.Threading.SpinWait>, você pode especificar um curto período de tempo para girar enquanto espera e, em seguida, gerar (por exemplo, aguardando ou em espera) somente se a condição não for atendida no tempo especificado.

Para obter mais informações, veja o artigo [SpinWait](spinwait.md) e a referência da API <xref:System.Threading.SpinWait>.

## <a name="see-also"></a>Confira também

- <xref:System.Collections.Concurrent?displayProperty=nameWithType>
- [Coleções com segurança de thread](../collections/thread-safe/index.md)
- [Objetos e recursos de Threading](threading-objects-and-features.md)
