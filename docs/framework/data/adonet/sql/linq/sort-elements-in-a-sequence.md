---
description: 'Saiba mais sobre: classificar elementos em uma sequência'
title: Elementos de tipo em uma sequência
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d59b93a9-50c8-4770-a114-d902f6a0ea76
ms.openlocfilehash: 337afe79826e9a9584a5fc3ed3980341dda1b4d8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803757"
---
# <a name="sort-elements-in-a-sequence"></a>Elementos de tipo em uma sequência

Use o operador de <xref:System.Linq.Enumerable.OrderBy%2A> para classificar uma sequência de acordo com um ou mais chaves.  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o é projetado para dar suporte à ordenação por tipos primitivos simples, como `string` , `int` e assim por diante. Não suporta classificação para várias classes avaliadas complexo, como tipos anônimos. Também não suporta tipos de dados de `byte` .  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir classe `Employees` a data de aluguer.  
  
 [!code-csharp[DLinqQueryExamples#20](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#20)]
 [!code-vb[DLinqQueryExamples#20](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#20)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa `where` para classificar `Orders` enviado a `London` por frete.  
  
 [!code-csharp[DLinqQueryExamples#21](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#21)]
 [!code-vb[DLinqQueryExamples#21](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#21)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir classe `Products` pelo preço unitário de mais alto para o menor.  
  
 [!code-csharp[DLinqQueryExamples#22](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#22)]
 [!code-vb[DLinqQueryExamples#22](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#22)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa um composto `OrderBy` para classificar por `Customers` cidade e em seguida pelo nome de contato.  
  
 [!code-csharp[DLinqQueryExamples#24](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#24)]
 [!code-vb[DLinqQueryExamples#24](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#24)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir classifica pedidos de `EmployeeID 1` por `ShipCountry` e, em seguida, pelo frete mais alto ao mais baixo.  
  
 [!code-csharp[DLinqQueryExamples#25](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#25)]
 [!code-vb[DLinqQueryExamples#25](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#25)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir combina <xref:System.Linq.Enumerable.OrderBy%2A>, <xref:System.Linq.Enumerable.Max%2A>, e os operadores de <xref:System.Linq.Enumerable.GroupBy%2A> para localizar `Products` que têm o preço unitário o maior em cada categoria, e classes no grupo pela ID da categoria  
  
 [!code-csharp[DLinqQueryExamples#26](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#26)]
 [!code-vb[DLinqQueryExamples#26](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#26)]  
  
 Se você executa a consulta anterior com o base de dados de exemplo Northwind, os resultados assemelhar-se-ão o seguinte:  
  
 `1`  
  
 `Côte de Blaye`  
  
 `2`  
  
 `Vegie-spread`  
  
 `3`  
  
 `Sir Rodney's Marmalade`  
  
 `4`  
  
 `Raclette Courdavault`  
  
 `5`  
  
 `Gnocchi di nonna Alice`  
  
 `6`  
  
 `Thüringer Rostbratwurst`  
  
 `7`  
  
 `Manjimup Dried Apples`  
  
 `8`  
  
 `Carnarvon Tigers`  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
