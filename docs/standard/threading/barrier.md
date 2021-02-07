---
description: 'Saiba mais sobre: barreira'
title: Barreira
ms.date: 09/14/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- synchronization primitives, Barrier
ms.assetid: 613a8bc7-6a28-4795-bd6c-1abd9050478f
ms.openlocfilehash: 7fca89e12ffe4575029e62ce042875dac286c81d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675501"
---
# <a name="barrier"></a>Barreira

Um <xref:System.Threading.Barrier?displayProperty=nameWithType> é um primitivo de sincronização definido pelo usuário que permite que vários threads (conhecidos como *participantes*) trabalhem simultaneamente em um algoritmo em fases. Cada participante executa até atingir o ponto de barreira no código. A barreira representa o final de uma fase de trabalho. Quando um participante alcança a barreira, ela é bloqueada até que todos os participantes atinjam a mesma barreira. Depois que todos os participantes tiverem chegado à barreira, opcionalmente, você poderá chamar uma ação pós-fase. Esta ação pós-fase pode ser usada para executar ações por um único thread enquanto todos os outros threads ainda estiverem bloqueados. Após a ação ser executada, todos os participantes serão desbloqueados.  
  
 O snippet de código a seguir mostra um padrão de barreira básica.  
  
 [!code-csharp[CDS_Barrier#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_barrier/cs/barrier.cs#02)]
 [!code-vb[CDS_Barrier#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_barrier/vb/barrier_vb.vb#02)]  
  
 Para um exemplo completo, veja [Como sincronizar operações simultâneas com uma barreira](how-to-synchronize-concurrent-operations-with-a-barrier.md).  
  
## <a name="adding-and-removing-participants"></a>Adicionar e remover participantes

 Ao criar uma instância de <xref:System.Threading.Barrier>, especifique o número de participantes. Você também pode adicionar ou remover participantes dinamicamente a qualquer momento. Por exemplo, se um participante resolver sua parte do problema, você poderá armazenar o resultado, parar a execução no thread e chamar <xref:System.Threading.Barrier.RemoveParticipant%2A?displayProperty=nameWithType> para diminuir o número de participantes na barreira. Quando você adiciona um participante chamando <xref:System.Threading.Barrier.AddParticipant%2A?displayProperty=nameWithType>, o valor de retorno especifica o número de fase atual, que pode ser útil para inicializar o trabalho do novo participante.  
  
## <a name="broken-barriers"></a>Barreiras interrompidas

 Os deadlocks podem ocorrer se um participante não conseguir alcançar a barreira. Para evitar esses deadlocks, use as sobrecargas do método <xref:System.Threading.Barrier.SignalAndWait%2A?displayProperty=nameWithType> para especificar um período de tempo limite e um token de cancelamento. Essas sobrecargas retorno um valor booliano que cada participante pode verificar antes de ele continuar para a próxima fase.  
  
## <a name="post-phase-exceptions"></a>Exceções pós-fase

 Se o representante da pós-fase lançar uma exceção, ele será encapsulado em um objeto <xref:System.Threading.BarrierPostPhaseException> que será, em seguida, propagado para todos os participantes.  
  
## <a name="barrier-versus-continuewhenall"></a>Barreira versus ContinueWhenAll

 As barreiras são especialmente úteis quando os threads estão executando várias fases em loops. Caso seu código requeira somente uma ou duas fases de trabalho, considere o uso de objetos <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> com qualquer tipo de junção implícita, incluindo:  
  
- <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType>  
  
- <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType>  
  
- <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>  
  
- <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType>  
  
 Para obter mais informações, consulte [Encadeando tarefas com tarefas de continuação](../parallel-programming/chaining-tasks-by-using-continuation-tasks.md).  
  
## <a name="see-also"></a>Consulte também

- [Objetos e recursos de threading](threading-objects-and-features.md)
- [Como: sincronizar operações simultâneas com uma barreira](how-to-synchronize-concurrent-operations-with-a-barrier.md)
