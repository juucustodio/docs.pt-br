---
description: 'Saiba mais sobre: retornar a União de conjunto de duas sequências'
title: Retornar a união de sequências de duas
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8b8bd3cb-86d4-4a3b-9906-61f68726dd1f
ms.openlocfilehash: 5541316560c05712e22c54f706b02d868fadb381
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662956"
---
# <a name="return-the-set-union-of-two-sequences"></a>Retornar a união de sequências de duas

Use o operador de <xref:System.Linq.Queryable.Union%2A> para retornar a união ajustada de duas sequências.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa <xref:System.Linq.Queryable.Union%2A> para retornar uma sequência de todos os países/regiões em que há `Customers` ou `Employees` .  
  
 [!code-csharp[DLinqQueryExamples#43](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#43)]
 [!code-vb[DLinqQueryExamples#43](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#43)]  
  
 No [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] , o <xref:System.Linq.Queryable.Union%2A> operador é definido para conjuntos de valores como a concatenação não ordenada dos conjuntos de multiconjuntos (efetivamente o resultado da [`UNION ALL`](/sql/t-sql/language-elements/set-operators-union-transact-sql) cláusula em SQL).

Para obter mais informações e exemplos, consulte <xref:System.Linq.Queryable.Union%2A?displayProperty=nameWithType> .
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
- [Conversão padrão de operador de consulta](standard-query-operator-translation.md)
