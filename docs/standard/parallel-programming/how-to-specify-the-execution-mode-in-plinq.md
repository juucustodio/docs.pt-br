---
description: 'Saiba mais sobre: como especificar o modo de execução no PLINQ'
title: 'Como: Especificar o modo de execução em PLINQ'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to use execution mode
ms.assetid: e52ff26c-c5d3-4fab-9fec-c937fb387963
ms.openlocfilehash: f897a7a2f60da1747b4cec253a98fd5608eb0f61
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641571"
---
# <a name="how-to-specify-the-execution-mode-in-plinq"></a>Como: Especificar o modo de execução em PLINQ

Este exemplo mostra como forçar o PLINQ a ignorar a heurística padrão e paralelizar uma consulta, independentemente da forma da consulta.  
  
> [!NOTE]
> Este exemplo destina-se a demonstrar o uso e pode não ser executado mais rápido do que a consulta LINQ to Objects sequencial equivalente. Para saber mais sobre agilização, confira [Noções básicas sobre agilização no PLINQ](understanding-speedup-in-plinq.md).  
  
## <a name="example"></a>Exemplo  

 [!code-csharp[PLINQ#22](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#22)]
 [!code-vb[PLINQ#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#22)]  
  
 O PLINQ foi projetado para explorar oportunidades de paralelização. No entanto, nem todas as consultas se beneficiam da execução paralela. Por exemplo, quando uma consulta contém um único delegado de usuário que faz pouco trabalho, a consulta geralmente é executada de forma mais rápida em sequência. A execução sequencial é mais rápida porque a sobrecarga envolvida na habilitação da execução de paralelização é mais cara do que a velocidade obtida. Portanto, o PLINQ não paraleliza automaticamente todas as consultas. Primeiro, examina a forma da consulta e os vários operadores que a compõem. Com base nessa análise, o PLINQ no modo de execução padrão pode decidir executar algumas das consultas em sequência ou todas elas. No entanto, em alguns casos, você pode saber mais sobre a consulta do que o PLINQ é capaz de determinar com base na análise. Por exemplo, você pode saber que um delegado é caro e que a consulta definitivamente se beneficiará da paralelização. Nesses casos, você pode usar o método <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> e especificar o valor <xref:System.Linq.ParallelExecutionMode.ForceParallelism> para instruir o PLINQ a sempre executar a consulta em paralelo.  
  
## <a name="compiling-the-code"></a>Compilando o código  

 Recorte e cole este código para o [Exemplo de Dados do PLINQ](plinq-data-sample.md) e chame o método `Main`.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Linq.ParallelEnumerable.AsSequential%2A>
- [LINQ paralelo (PLINQ)](introduction-to-plinq.md)
