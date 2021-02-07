---
description: 'Saiba mais sobre: Method-Based exemplos de sintaxe de consulta: ordenação'
title: 'Exemplos de sintaxe da consulta com base em método: Classificação'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5d21b178-d731-471a-8534-1f8184a2ef06
ms.openlocfilehash: 7b1c67ba66f549e82a57b5b34c645d36d1255a14
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696692"
---
# <a name="method-based-query-syntax-examples-ordering"></a>Exemplos de sintaxe da consulta com base em método: Classificação

Os exemplos neste tópico demonstram como usar o <xref:System.Linq.Enumerable.ThenBy%2A> método para consultar o [modelo de vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) usando a sintaxe de consulta baseada em método. O Modelo de vendas AdventureWorks usado nesses exemplos é criado a partir das tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="thenby"></a>ThenBy  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir na sintaxe da consulta com base em método usa <xref:System.Linq.Queryable.OrderBy%2A> e <xref:System.Linq.Queryable.ThenBy%2A> para retornar uma lista de contatos ordenados por sobrenome e em seguida pelo nome.  
  
 [!code-csharp[DP L2E Examples#OrderByThenBy_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbythenby_mq)]
 [!code-vb[DP L2E Examples#OrderByThenBy_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbythenby_mq)]  
  
## <a name="thenbydescending"></a>ThenByDescending  
  
### <a name="example"></a>Exemplo  

 O seguinte exemplo usa os métodos de <xref:System.Linq.Queryable.OrderBy%2A> e de <xref:System.Linq.Queryable.ThenByDescending%2A> para o primeiro tipo pelo custo da tabela e em seguida, executar uma descida meio de nomes do produto.  
  
 [!code-csharp[DP L2E Examples#ThenByDescending_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#thenbydescending_mq)]
 [!code-vb[DP L2E Examples#ThenByDescending_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#thenbydescending_mq)]  
  
## <a name="see-also"></a>Consulte também

- [Consultas no LINQ to Entities](queries-in-linq-to-entities.md)
