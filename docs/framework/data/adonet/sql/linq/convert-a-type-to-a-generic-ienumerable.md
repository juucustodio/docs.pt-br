---
description: 'Saiba mais sobre: converter um tipo em um IEnumerable genérico'
title: Converter um tipo genérico a um IEnumerable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 64774fb5-7447-4296-ad3b-8a94346f99a1
ms.openlocfilehash: 9be9022bce84808e18514937116ea962065dc1a8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712513"
---
# <a name="convert-a-type-to-a-generic-ienumerable"></a>Converter um tipo genérico a um IEnumerable

Use <xref:System.Linq.Enumerable.AsEnumerable%2A> para retornar o argumento tipado como `IEnumerable`genérico.  
  
## <a name="example"></a>Exemplo  

 Nesse exemplo, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] (usando `Query`genérico padrão) tentaria converter a consulta SQL e executados no servidor. Mas a cláusula de `where` referencia um método do lado do cliente definido pelo usuário (`isValidProduct`), que não pode ser convertido para SQL.  
  
 A solução é especificar a implementação genérica do lado do cliente de <xref:System.Collections.Generic.IEnumerable%601> de `where` para substituir <xref:System.Linq.IQueryable%601>genérico. Você faz isso chamando o operador de <xref:System.Linq.Enumerable.AsEnumerable%2A> .  
  
 [!code-csharp[DLinqQueryExamples#46](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#46)]
 [!code-vb[DLinqQueryExamples#46](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#46)]  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
