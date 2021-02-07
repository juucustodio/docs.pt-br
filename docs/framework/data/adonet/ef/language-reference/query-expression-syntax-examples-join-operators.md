---
description: 'Saiba mais sobre: exemplos de sintaxe de expressão de consulta: operadores de junção'
title: 'Exemplos de sintaxe de expressão de consulta: operadores de junção'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 343e8dda-70b2-409d-9334-ce9a880c3cea
ms.openlocfilehash: 01ca3157ef13097c5c89ac1e6bafd03873c05977
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696198"
---
# <a name="query-expression-syntax-examples-join-operators"></a>Exemplos de sintaxe de expressão de consulta: operadores de junção

A junção é uma operação importante em consultas que usam fontes de dados de destino que não têm nenhuma relação navegável entre si, como, por exemplo, as tabelas do banco de dados relacional. Uma junção de duas fontes de dados é a associação de objetos em uma fonte de dados com objetos que compartilham um atributo comum em outra fonte de dados. Para obter mais informações, consulte [visão geral de operadores de consulta padrão](/previous-versions/visualstudio/visual-studio-2013/bb397896(v=vs.120)).  
  
 Os exemplos neste tópico demonstram como usar os <xref:System.Linq.Enumerable.GroupJoin%2A> métodos e <xref:System.Linq.Enumerable.Join%2A> para consultar o [modelo de vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) usando a sintaxe de expressão de consulta. O Modelo de vendas AdventureWorks usado nesses exemplos é criado a partir das tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="groupjoin"></a>GroupJoin  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir executa um <xref:System.Linq.Enumerable.GroupJoin%2A> nas tabelas SalesOrderHeader e SalesOrderDetail para localizar o número de pedidos por cliente. Um group join é o equivalente a um left outer join, que retorna cada elemento da primeira fonte de dados (esquerda), mesmo se nenhum elemento correlacionado estiver na outra fonte de dados.  
  
 [!code-csharp[DP L2E Examples#GroupJoin2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#groupjoin2)]
 [!code-vb[DP L2E Examples#GroupJoin2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#groupjoin2)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir executa um <xref:System.Linq.Enumerable.GroupJoin%2A> nas tabelas Contact e SalesOrderHeader para localizar o número de pedidos por contato. A contagem do pedido e as identificações para cada contato são exibidos.  
  
 [!code-csharp[DP L2E Examples#GroupJoin](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#groupjoin)]
 [!code-vb[DP L2E Examples#GroupJoin](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#groupjoin)]  
  
## <a name="join"></a>Join  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir realiza uma união das tabelas SalesOrderHeader e SalesOrderDetail para obter pedidos online do mês de agosto.  
  
 [!code-csharp[DP L2E Examples#Join](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#join)]
 [!code-vb[DP L2E Examples#Join](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#join)]  
  
## <a name="see-also"></a>Consulte também

- [Consultas no LINQ to Entities](queries-in-linq-to-entities.md)
