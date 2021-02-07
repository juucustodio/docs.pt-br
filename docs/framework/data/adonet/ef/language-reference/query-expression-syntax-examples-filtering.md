---
description: 'Saiba mais sobre: exemplos de sintaxe de expressão de consulta: filtragem'
title: 'Exemplos de sintaxe de expressão de consulta: filtragem'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c27cb89c-1c1d-4988-9f38-950eda3cb275
ms.openlocfilehash: f8bc2d08f7a8916ccbd2884ff9a9af616b2118f6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696224"
---
# <a name="query-expression-syntax-examples-filtering"></a>Exemplos de sintaxe de expressão de consulta: filtragem

Os exemplos neste tópico demonstram como usar os `Where` métodos e `Where…Contains` para consultar o [modelo de vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) usando a sintaxe de expressão de consulta. Observação, onde...`Contains` Não pode ser usado como parte de uma [consulta compilada](compiled-queries-linq-to-entities.md).  
  
 O Modelo de vendas AdventureWorks usado nesses exemplos é criado a partir das tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="where"></a>Where  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir retorna todos os pedidos online.  
  
 [!code-csharp[DP L2E Examples#Where1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where1)]
 [!code-vb[DP L2E Examples#Where1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where1)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir retorna os pedidos onde a quantidade é maior que 2 e menor que 6.  
  
 [!code-csharp[DP L2E Examples#Where2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where2)]
 [!code-vb[DP L2E Examples#Where2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where2)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir retorna todos os produtos vermelhos.  
  
 [!code-csharp[DP L2E Examples#Where3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where3)]
 [!code-vb[DP L2E Examples#Where3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where3)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método `Where` para localizar os pedidos que foram feitos depois de 1° de dezembro de 2003 e, em seguida, usa a propriedade de navegação `order.SalesOrderDetail` para obter os detalhes de cada pedido.  
  
 [!code-csharp[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#wherenavproperty)]
 [!code-vb[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#wherenavproperty)]  
  
## <a name="wherecontains"></a>Where…Contains  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa uma matriz como parte de uma cláusula `Where…Contains` para localizar todos os produtos que têm um `ProductModelID` que coincide com um valor na matriz.  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#1)]
 [!code-vb[DP L2E ArraysAndListsInQueries#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#1)]  
  
> [!NOTE]
> Como parte do predicado em uma cláusula `Where…Contains`, você pode usar um <xref:System.Array>, <xref:System.Collections.Generic.List%601> ou uma coleção de qualquer tipo que implemente a interface de <xref:System.Collections.Generic.IEnumerable%601>. Você também pode declarar e inicializar uma coleção em uma consulta LINQ to Entities. Consulte o próximo exemplo para obter mais informações.  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir declara e inicializa matrizes em uma cláusula `Where…Contains` para localizar todos os produtos que têm um `ProductModelID` ou `Size` que coincidem com valores na matriz.  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#2)]
 [!code-vb[DP L2E ArraysAndListsInQueries#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- [Consultas no LINQ to Entities](queries-in-linq-to-entities.md)
