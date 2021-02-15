---
description: 'Saiba mais sobre: como acelerar corpos pequenos de loops'
title: 'Como: Acelerar corpos de loop pequenos'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to speed up
ms.assetid: c7a66677-cb59-4cbf-969a-d2e8fc61a6ce
ms.openlocfilehash: 6505aae545959266e94fd866f7e4cd8643cffb65
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99629507"
---
# <a name="how-to-speed-up-small-loop-bodies"></a>Como: Acelerar corpos de loop pequenos

Quando um loop <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> tem um corpo pequeno, ele pode executar mais lentamente do que o loop sequencial equivalente, como o loop [para](../../csharp/language-reference/keywords/for.md) em c# e o loop [Para](/previous-versions/visualstudio/visual-studio-2008/44kykk21(v=vs.90)) no Visual Basic. O desempenho mais lento é causado pela sobrecarga envolvida no particionamento dos dados e do custo de invocação de um representante em cada iteração do loop. Para resolver esses cenários, a classe <xref:System.Collections.Concurrent.Partitioner> fornece o método <xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=nameWithType>, que permite que você forneça um loop sequencial do corpo do representante, de modo que o representante seja chamado apenas uma vez por partição, em vez de uma vez por iteração. Para saber mais, veja [Particionadores personalizados para PLINQ e TPL](custom-partitioners-for-plinq-and-tpl.md).  
  
## <a name="example"></a>Exemplo  

 [!code-csharp[TPL_Partitioners#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioner01.cs#01)]
 [!code-vb[TPL_Partitioners#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionercreate01.vb#01)]  
  
 A abordagem demonstrada neste exemplo é útil quando o loop executa uma quantidade mínima de trabalho. Como o trabalho se torna mais dispendioso computacionalmente, você provavelmente obterá um desempenho igual ou melhor usando um loop <xref:System.Threading.Tasks.Parallel.For%2A> ou <xref:System.Threading.Tasks.Parallel.ForEach%2A> com o particionador padrão.  
  
## <a name="see-also"></a>Consulte também

- [Paralelismo de dados](data-parallelism-task-parallel-library.md)
- [Particionadores personalizados para PLINQ e TPL](custom-partitioners-for-plinq-and-tpl.md)
- [Iteradores (C#)](../../csharp/programming-guide/concepts/iterators.md)
- [Iteradores (Visual Basic)](../../visual-basic/programming-guide/concepts/iterators.md)
- [Expressões lambda em PLINQ e TPL](lambda-expressions-in-plinq-and-tpl.md)
