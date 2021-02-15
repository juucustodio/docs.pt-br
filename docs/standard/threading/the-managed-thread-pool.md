---
title: O pool de threads gerenciados
description: Saiba mais sobre o pool de threads do .NET que fornece threads de trabalho em segundo plano
ms.date: 08/02/2018
helpviewer_keywords:
- thread pooling [.NET]
- thread pools [.NET]
- threading [.NET], thread pool
- threading [.NET], pooling
ms.assetid: 2be05b06-a42e-4c9d-a739-96c21d673927
ms.openlocfilehash: 9bc90acd6d7e1bef81e767ce8c257fed78322554
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826177"
---
# <a name="the-managed-thread-pool"></a>O pool de threads gerenciados

A classe <xref:System.Threading.ThreadPool?displayProperty=nameWithType> fornece ao seu aplicativo um pool de threads de trabalho gerenciados pelo sistema, permitindo que você se concentre em tarefas de aplicativo, e não no gerenciamento de threads. Se você tiver tarefas curtas que exigem processamento em segundo plano, o pool de threads gerenciados será uma maneira fácil de aproveitar os vários threads. O uso do pool de threads é significativamente mais fácil no Framework 4 e versões posteriores, já que você pode criar objetos <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601> que executam tarefas assíncronas em threads do pool de threads.  
  
O .NET usa threads do pool de threads para muitos fins, incluindo em operações de [TPL (Biblioteca de Paralelismo de Tarefas)](../parallel-programming/task-parallel-library-tpl.md), na conclusão de E/S assíncrona, em retornos de chamada [timer](timers.md), em operações de espera registradas, em chamadas de método assíncrono usando delegados e em conexões de soquete <xref:System.Net?displayProperty=nameWithType>.  

## <a name="thread-pool-characteristics"></a>Características do pool de threads

Os threads de pool de threads são threads de [segundo plano](foreground-and-background-threads.md). Cada thread usa o tamanho da pilha padrão, é executado com prioridade padrão e está no apartamento de vários threads. Depois que um thread do pool conclui sua tarefa, ele é retornado para uma fila de threads em espera. A partir desse momento, ele pode ser reutilizado. Essa reutilização permite que os aplicativos evitem o custo de criação de um novo thread para cada tarefa.
  
Há apenas um pool de threads por processo.  
  
### <a name="exceptions-in-thread-pool-threads"></a>Exceções em threads do pool de threads

Exceções sem tratamento nos threads do pool de threads encerram o processo. Há três exceções a essa regra:  
  
- Um <xref:System.Threading.ThreadAbortException?displayProperty=nameWithType> é gerado em um thread do pool de threads porque <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> foi chamado.  
- Um <xref:System.AppDomainUnloadedException?displayProperty=nameWithType> é gerado em um thread do pool de threads porque o domínio do aplicativo está sendo descarregado.  
- O CLR ou um processo de host encerra o thread.  
  
Para obter mais informações, consulte [exceções em threads gerenciados](exceptions-in-managed-threads.md).  
  
### <a name="maximum-number-of-thread-pool-threads"></a>Número máximo de threads do pool de threads

O número de operações que podem ser enfileiradas para o pool de threads é limitado apenas pela memória disponível. No entanto, o pool de threads limita o número de threads que podem estar ativos no processo simultaneamente. Se todos os threads do pool de threads estiverem ocupados, itens de trabalho adicionais serão enfileirados até que os threads para os executar se tornem disponíveis. O tamanho padrão do pool de threads para um processo depende de vários fatores, como o tamanho do espaço de endereço virtual. Um processo pode chamar o método <xref:System.Threading.ThreadPool.GetMaxThreads%2A?displayProperty=nameWithType> para determinar o número de threads.  
  
Você pode controlar o número máximo de threads usando os métodos <xref:System.Threading.ThreadPool.GetMaxThreads%2A?displayProperty=nameWithType> e <xref:System.Threading.ThreadPool.SetMaxThreads%2A?displayProperty=nameWithType>.  

> [!NOTE]
> O código que hospeda o Common Language Runtime pode definir o tamanho usando o [`ICorThreadpool::CorSetMaxThreads`](../../framework/unmanaged-api/hosting/icorthreadpool-corsetmaxthreads-method.md) método.  
  
### <a name="thread-pool-minimums"></a>Valores mínimos no pool de threads

O pool de threads fornece novos threads de trabalho ou threads de conclusão de E/S sob demanda, até atingir um mínimo especificado para cada categoria. Você pode usar o método <xref:System.Threading.ThreadPool.GetMinThreads%2A?displayProperty=nameWithType> para obter esses valores mínimos.  
  
> [!NOTE]
> Quando a demanda é baixa, o número real de threads do pool de threads pode ficar abaixo dos valores mínimos.  
  
Quando o mínimo é atingido, o pool de threads pode criar threads adicionais ou aguardar a conclusão de algumas tarefas. O pool de threads cria e destrói threads de trabalho para otimizar a taxa de transferência, que é definida como o número de tarefas concluídas por unidade de tempo. Pouquíssimos threads podem não fazer um uso ideal dos recursos disponíveis, enquanto muitos threads podem aumentar a contenção de recursos.  
  
> [!CAUTION]
> Use o método <xref:System.Threading.ThreadPool.SetMinThreads%2A?displayProperty=nameWithType> para aumentar o número mínimo de threads ociosos. No entanto, o aumento desnecessário desses valores pode causar problemas de desempenho. Se muitas tarefas começarem ao mesmo tempo, todas elas podem parecer lentas. Na maioria dos casos, o pool de threads terá um desempenho melhor com seu próprio algoritmo de alocação de threads.  

## <a name="using-the-thread-pool"></a>Usando o pool de threads

A maneira mais fácil de usar o pool de threads é usar a [TPL (biblioteca paralela de tarefas)](../parallel-programming/task-parallel-library-tpl.md). Por padrão, tipos de TPL como <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601> usam threads do pool de threads para executar tarefas.

Você também pode usar o pool de threads chamando <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=nameWithType> de código gerenciado (ou [`ICorThreadpool::CorQueueUserWorkItem`](../../framework/unmanaged-api/hosting/icorthreadpool-corqueueuserworkitem-method.md) de código não gerenciado) e passando um <xref:System.Threading.WaitCallback?displayProperty=nameWithType> delegado que representa o método que executa a tarefa.

Outra maneira de usar o pool de threads é enfileirando itens de trabalho relacionados a uma operação de espera usando o método <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> e passando um <xref:System.Threading.WaitHandle?displayProperty=nameWithType> que, quando sinalizado ou após tempo limite, chama o método representado pelo delegado <xref:System.Threading.WaitOrTimerCallback?displayProperty=nameWithType>. Os threads do pool de thread são usados para invocar métodos de retorno de chamada.  

Para os exemplos, verifique as páginas de API referenciadas.
  
## <a name="skipping-security-checks"></a>Ignorando as verificações de segurança

O pool de threads também fornece os métodos <xref:System.Threading.ThreadPool.UnsafeQueueUserWorkItem%2A?displayProperty=nameWithType> e <xref:System.Threading.ThreadPool.UnsafeRegisterWaitForSingleObject%2A?displayProperty=nameWithType>. Use estes métodos somente quando você tiver certeza de que a pilha do chamador é irrelevante a qualquer verificação de segurança executada durante a execução da tarefa em fila. <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=nameWithType> e <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> capturam a pilha do chamador, que é mesclada na pilha do thread do pool de threads quando o thread começa a executar uma tarefa. Se uma verificação de segurança for necessária, toda a pilha deverá ser verificada. Embora a verificação forneça segurança, também tem um custo de desempenho.  

## <a name="when-not-to-use-thread-pool-threads"></a>Quando não usar o thread do pool de threads

Há várias situações nas quais é apropriado criar e gerenciar seus próprios threads em vez de usar os threads do pool de threads:  
  
- Você precisa de um thread em primeiro plano.  
- Você precisa que um thread tenha uma prioridade específica.  
- Há tarefas que causam o bloqueio do thread por longos períodos. O pool de threads tem um número máximo de threads, portanto, a existência de muitos threads do pool de threads bloqueados pode impedir a inicialização das tarefas.  
- Você precisa colocar os threads em um apartamento de thread único. Todos os threads <xref:System.Threading.ThreadPool> estão no apartamento de vários threads.  
- Você precisa ter uma identidade estável associada ao thread, ou dedicar um thread a uma tarefa.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Threading.ThreadPool?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>
- [Biblioteca de tarefas paralelas (TPL)](../parallel-programming/task-parallel-library-tpl.md)
- [Como: Retornar um valor de uma tarefa](../parallel-programming/how-to-return-a-value-from-a-task.md)
- [Threading de objetos e recursos](threading-objects-and-features.md)
- [Threads e threading](threads-and-threading.md)
- [E/s de arquivo assíncrono](../io/asynchronous-file-i-o.md)
- [Temporizadores](timers.md)
