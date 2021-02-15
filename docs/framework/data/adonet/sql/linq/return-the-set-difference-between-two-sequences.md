---
description: 'Saiba mais sobre: retornar a diferença de conjunto entre duas sequências'
title: Retornar a diferença entre duas sequências ajustada
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 62efb546-c898-408f-af21-36e7c6fed217
ms.openlocfilehash: 6836195ac4e1ee678fd3e8089e7c341f7dd247e8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662970"
---
# <a name="return-the-set-difference-between-two-sequences"></a>Retornar a diferença entre duas sequências ajustada

Use o operador de <xref:System.Linq.Queryable.Except%2A> para retornar a diferença entre duas ajustada sequências.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa <xref:System.Linq.Queryable.Except%2A> para retornar uma sequência de todos os países/regiões nos quais o `Customers` Live, mas no qual não há `Employees` tempo.  
  
 [!code-csharp[DLinqQueryExamples#41](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#41)]
 [!code-vb[DLinqQueryExamples#41](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#41)]  
  
 Em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], a operação de <xref:System.Linq.Queryable.Except%2A> é bem definido somente em conjuntos. A semântica de multisets é indefinida.  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
- [Conversão padrão de operador de consulta](standard-query-operator-translation.md)
