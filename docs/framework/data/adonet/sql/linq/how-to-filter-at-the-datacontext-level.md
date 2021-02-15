---
description: 'Saiba mais sobre: como filtrar no nível de DataContext'
title: 'Como: filtrar no nível de DataContext'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 15505cd7-0df2-427a-9f86-e0f96f60ee2e
ms.openlocfilehash: ffb287ac1ef8cc19044ec3d519e745f905fe213d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785972"
---
# <a name="how-to-filter-at-the-datacontext-level"></a>Como: filtrar no nível de DataContext

Você pode filtrar `EntitySets` em `DataContext` nível. Como filtros se aplicam a todas as consultas feitas com essa instância de <xref:System.Data.Linq.DataContext> .  
  
## <a name="example"></a>Exemplo  

 No exemplo a seguir, <xref:System.Data.Linq.DataLoadOptions.AssociateWith%28System.Linq.Expressions.LambdaExpression%29?displayProperty=nameWithType> é usado para filtrar os pedidos pré-compilação para clientes carregados por `ShippedDate`.  
  
 [!code-csharp[DLinqQueryConcepts#10](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#10)]
 [!code-vb[DLinqQueryConcepts#10](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#10)]  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
