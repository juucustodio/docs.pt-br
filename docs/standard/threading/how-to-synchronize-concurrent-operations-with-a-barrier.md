---
description: 'Saiba mais sobre: como sincronizar operações simultâneas com uma barreira'
title: Como sincronizar operações simultâneas com uma barreira
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Barrier, how to use
ms.assetid: e1a253ff-e0fb-4df8-95ff-d01a90d4cb19
ms.openlocfilehash: 7cef2598171f31ddb5685ff8f1734ed705a4752b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99666752"
---
# <a name="how-to-synchronize-concurrent-operations-with-a-barrier"></a>Como sincronizar operações simultâneas com uma barreira

O exemplo a seguir mostra como sincronizar tarefas simultâneas com uma <xref:System.Threading.Barrier>.  
  
## <a name="example"></a>Exemplo  

 O objetivo do programa a seguir é contar quantas iterações (ou fases) são necessárias para dois threads para que cada um localize sua metade da solução na mesma fase usando um algoritmo aleatório para reorganizar as palavras. Após cada thread ter misturado suas palavras, a operação de pós-fase de barreira comparará os dois resultados para ver se a frase completa foi renderizada na ordem de palavras correta.  
  
 [!code-csharp[CDS_Barrier#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_barrier/cs/barrier.cs#01)]
 [!code-vb[CDS_Barrier#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_barrier/vb/barrier_vb.vb#01)]  
  
 Uma <xref:System.Threading.Barrier> é um objeto que impede que as tarefas individuais em uma operação paralela continuem até que todas as tarefas atinjam a barreira. É útil quando uma operação paralela ocorre em fases e cada fase requer a sincronização entre as tarefas. Neste exemplo, há duas fases para a operação. Na primeira fase, cada tarefa preenche sua seção do buffer com dados. Quando cada tarefa termina de preencher sua seção, a tarefa sinaliza a barreira que ela está pronta para continuar e, em seguida, aguarda. Quando todas as tarefas sinalizarem a barreira, elas serão desbloqueadas e a segunda fase começará. A barreira é necessária porque a segunda fase requer que cada tarefa tenha acesso a todos os dados que foram gerados até este ponto. Sem a barreira, as primeiras tarefas a serem concluídas podem tentar ler de buffers que ainda não foram preenchidos por outras tarefas. Você pode sincronizar qualquer número das fases dessa maneira.  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de dados para programação paralela](../parallel-programming/data-structures-for-parallel-programming.md)
