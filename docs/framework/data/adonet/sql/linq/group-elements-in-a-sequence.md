---
description: 'Saiba mais sobre: agrupar elementos em uma sequência'
title: Agrupar os elementos em uma sequência
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1d50c8b4-f550-4775-bbb6-eab6e874cb43
ms.openlocfilehash: bc9a4d042ed0edb090f0530ebb24d99a5390c882
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786063"
---
# <a name="group-elements-in-a-sequence"></a>Agrupar os elementos em uma sequência

O operador de <xref:System.Linq.Enumerable.GroupBy%2A> agrupa elementos de uma sequência. Os exemplos usam o base de dados Northwind.  
  
> [!NOTE]
> Valores nulos de coluna em consultas de <xref:System.Linq.Enumerable.GroupBy%2A> podem lançar as vezes <xref:System.InvalidOperationException>. Para obter mais informações, consulte a seção "GroupBy InvalidOperationException" de [solução de problemas](troubleshooting.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir divide `Products` por `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#27](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#27)]
 [!code-vb[DLinqQueryExamples#27](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#27)]  
  
## <a name="example"></a>Exemplo  

 Os seguintes usa <xref:System.Linq.Enumerable.Max%2A> de exemplo encontrar o preço unitário máximo para cada `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#28](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#28)]
 [!code-vb[DLinqQueryExamples#28](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#28)]  
  
## <a name="example"></a>Exemplo  

 Os seguintes o exemplo usa especificam intermediária para localizar `UnitPrice` médio para cada `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#29](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#29)]
 [!code-vb[DLinqQueryExamples#29](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#29)]  
  
## <a name="example"></a>Exemplo  

 Os seguintes usa <xref:System.Linq.Queryable.Sum%2A> de exemplo encontrar `UnitPrice` total para cada `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#30](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#30)]
 [!code-vb[DLinqQueryExamples#30](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#30)]  
  
## <a name="example"></a>Exemplo  

 Os seguintes usa <xref:System.Linq.Queryable.Count%2A> de exemplo encontrar o número de `Products` descontinuado em cada `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#31](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#31)]
 [!code-vb[DLinqQueryExamples#31](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#31)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa uma cláusula de `where` para localizar todas as categorias que tem pelo menos 10 produtos.  
  
 [!code-csharp[DLinqQueryExamples#32](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#32)]
 [!code-vb[DLinqQueryExamples#32](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#32)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir agrupa produtos por `CategoryID` e por `SupplierID`.  
  
 [!code-csharp[DLinqQueryExamples#33](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#33)]
 [!code-vb[DLinqQueryExamples#33](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#33)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir retorna duas sequências de produtos. A primeira sequência contém classes com preço unitário menor ou igual a 10. A segunda sequência contém classes com o preço unitário maior que 10.  
  
 [!code-csharp[DLinqQueryExamples#34](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#34)]
 [!code-vb[DLinqQueryExamples#34](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#34)]  
  
## <a name="example"></a>Exemplo  

 O operador de <xref:System.Linq.Queryable.GroupBy%2A> pode levar apenas um único argumento principal. Se você precisará se agrupar por mais de uma chave, você deve criar um tipo anônimo, como no exemplo a seguir:  
  
 [!code-csharp[DLinqQueryExamples#35](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#35)]
 [!code-vb[DLinqQueryExamples#35](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#35)]  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
