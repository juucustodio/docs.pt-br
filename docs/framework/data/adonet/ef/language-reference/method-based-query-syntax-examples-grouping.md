---
description: 'Saiba mais sobre: Method-Based exemplos de sintaxe de consulta: agrupamento'
title: 'Exemplos de sintaxe da consulta com base em método: Clustering'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cb23c25c-1075-4cc3-a8ff-4db72e536c0d
ms.openlocfilehash: dd605076a425207aa379216a9e8dba60eaeebc29
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99673499"
---
# <a name="method-based-query-syntax-examples-grouping"></a>Exemplos de sintaxe da consulta com base em método: Clustering

Os exemplos neste tópico mostram como usar o `GroupBy` método para consultar o [modelo de vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) usando a sintaxe de consulta baseada em método. Modelo de Vendas de exemplo AdventureWorks que é usada nesses exemplos é compilado de tabelas de contato, o endereço, do produto, de SalesOrderHeader, e o SalesOrderDetail na base de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método de `GroupBy` para retornar objetos de `Address` que são agrupados pelo código postal. Os resultados são projetados em um tipo anônimo.  
  
 [!code-csharp[DP L2E Examples#GroupBySimple3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#groupbysimple3_mq)]
 [!code-vb[DP L2E Examples#GroupBySimple3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#groupbysimple3_mq)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método de `GroupBy` para retornar objetos de `Contact` que são agrupados pela primeira letra do último contato. Os resultados são também classificados pela primeira letra do sobrenome e projetados em um tipo anônimo.  
  
 [!code-csharp[DP L2E Examples#GroupBySimple2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#groupbysimple2_mq)]
 [!code-vb[DP L2E Examples#GroupBySimple2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#groupbysimple2_mq)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método de `GroupBy` para retornar objetos de `SalesOrderHeader` que são agrupados pela identificação do cliente O número de vendas para cada cliente também é retornado.  
  
 [!code-csharp[DP L2E Examples#GroupByCount_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#groupbycount_mq)]
 [!code-vb[DP L2E Examples#GroupByCount_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#groupbycount_mq)]  
  
## <a name="see-also"></a>Consulte também

- [Consultas no LINQ to Entities](queries-in-linq-to-entities.md)
