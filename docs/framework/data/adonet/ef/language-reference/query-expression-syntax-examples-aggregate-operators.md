---
description: 'Saiba mais sobre: exemplos de sintaxe de expressão de consulta: operadores de agregação'
title: 'Consulte exemplos de sintaxe de expressão: Operadores agregados'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d729120c-4c1b-4f34-bbe9-33694fca2dde
ms.openlocfilehash: c0fd9c3faf770a00a54341cf3718c2dda91a4d7b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767928"
---
# <a name="query-expression-syntax-examples-aggregate-operators"></a>Consulte exemplos de sintaxe de expressão: Operadores agregados

Os exemplos neste tópico demonstram como usar os <xref:System.Linq.Enumerable.Average%2A> métodos, <xref:System.Linq.Enumerable.Count%2A> , <xref:System.Linq.Enumerable.Max%2A> , <xref:System.Linq.Enumerable.Min%2A> e <xref:System.Linq.Enumerable.Sum%2A> para consultar o modelo de [vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) usando a sintaxe de expressão de consulta. O Modelo de vendas AdventureWorks usado nesses exemplos é criado a partir das tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="average"></a>Média  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método <xref:System.Linq.Enumerable.Average%2A> para localizar o preço médio da lista de produtos de cada estilo.  
  
 [!code-csharp[DP L2E Examples#Average2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#average2_mq)]
 [!code-vb[DP L2E Examples#Average2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#average2_mq)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa <xref:System.Linq.Enumerable.Average%2A> para obter o total vencido médio para cada identificação de contatos  
  
 [!code-csharp[DP L2E Examples#AverageGrouped_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#averagegrouped_mq)]
 [!code-vb[DP L2E Examples#AverageGrouped_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#averagegrouped_mq)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa <xref:System.Linq.Enumerable.Average%2A> para obter os pedidos com o total vencido médio para cada contato.  
  
 [!code-csharp[DP L2E Examples#AverageElements_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#averageelements_mq)]
 [!code-vb[DP L2E Examples#AverageElements_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#averageelements_mq)]  
  
## <a name="count"></a>Contagem  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa <xref:System.Linq.Enumerable.Count%2A> para retornar uma lista de IDs de contato e quantos pedidos cada um possui.  
  
 [!code-csharp[DP L2E Examples#CountNested](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#countnested)]
 [!code-vb[DP L2E Examples#CountNested](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#countnested)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir agrupa produtos pela cor e usa <xref:System.Linq.Enumerable.Count%2A> para retornar o número de produtos em cada grupo de cor.  
  
 [!code-csharp[DP L2E Examples#CountGrouped](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#countgrouped)]
 [!code-vb[DP L2E Examples#CountGrouped](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#countgrouped)]  
  
## <a name="max"></a>Max  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método <xref:System.Linq.Enumerable.Max%2A> para obter o maior valor total para cada ID de contato.  
  
 [!code-csharp[DP L2E Examples#MaxGrouped_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#maxgrouped_mq)]
 [!code-vb[DP L2E Examples#MaxGrouped_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#maxgrouped_mq)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método <xref:System.Linq.Enumerable.Max%2A> para obter os pedidos com o maior valor total para cada ID de contato.  
  
 [!code-csharp[DP L2E Examples#MaxElements_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#maxelements_mq)]
 [!code-vb[DP L2E Examples#MaxElements_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#maxelements_mq)]  
  
## <a name="min"></a>Min  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método <xref:System.Linq.Enumerable.Min%2A> para obter o menor valor total para cada ID de contato.  
  
 [!code-csharp[DP L2E Examples#MinGrouped_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#mingrouped_mq)]
 [!code-vb[DP L2E Examples#MinGrouped_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#mingrouped_mq)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método <xref:System.Linq.Enumerable.Min%2A> para obter os pedidos com o menor valor total para cada contato.  
  
 [!code-csharp[DP L2E Examples#MinElements_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#minelements_mq)]
 [!code-vb[DP L2E Examples#MinElements_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#minelements_mq)]  
  
## <a name="sum"></a>Somar  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método <xref:System.Linq.Enumerable.Sum%2A> para obter o valor total para cada ID de contato.  
  
 [!code-csharp[DP L2E Examples#SumGrouped_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#sumgrouped_mq)]
 [!code-vb[DP L2E Examples#SumGrouped_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#sumgrouped_mq)]  
  
## <a name="see-also"></a>Consulte também

- [Consultas no LINQ to Entities](queries-in-linq-to-entities.md)
