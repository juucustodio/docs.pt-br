---
description: 'Saiba mais sobre: como combinar consultas LINQ paralelas e sequenciais'
title: 'Como: combinar consultas LINQ paralelas e sequenciais'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel queries, combine parallel and sequential
ms.assetid: 1167cfe6-c8aa-4096-94ba-c66c3a4edf4c
ms.openlocfilehash: b3ff966b944516bed6cfb4cacd32cb550455fea9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99702061"
---
# <a name="how-to-combine-parallel-and-sequential-linq-queries"></a>Como: combinar consultas LINQ paralelas e sequenciais

Este exemplo mostra como usar o método <xref:System.Linq.ParallelEnumerable.AsSequential%2A> para instruir o PLINQ para processar todos os operadores subsequentes na consulta em sequência. Embora o processamento sequencial seja geralmente mais lento do que o paralelo, às vezes é necessário produzir resultados corretos.  
  
> [!NOTE]
> Este exemplo destina-se a demonstrar o uso e pode não ser executado mais rápido do que a consulta LINQ to Objects sequencial equivalente. Para saber mais sobre agilização, confira [Noções básicas sobre agilização no PLINQ](understanding-speedup-in-plinq.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra um cenário em que <xref:System.Linq.ParallelEnumerable.AsSequential%2A> é necessário, ou seja, para preservar a ordem que foi estabelecida em uma cláusula anterior da consulta.  
  
 [!code-csharp[PLINQ#24](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#24)]
 [!code-vb[PLINQ#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#24)]  
  
## <a name="compiling-the-code"></a>Compilando o código  

 Para compilar e executar esse código, Cole-o no projeto de [exemplo de dados do PLINQ](plinq-data-sample.md) , adicione uma linha para chamar o método `Main` e pressione **F5**.  
  
## <a name="see-also"></a>Consulte também

- [LINQ paralelo (PLINQ)](introduction-to-plinq.md)
