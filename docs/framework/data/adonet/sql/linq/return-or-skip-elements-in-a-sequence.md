---
description: 'Saiba mais sobre: retornar ou ignorar elementos em uma sequência'
title: Elementos Return ou Skip em uma sequência
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 81a31acd-e0f1-4bca-9a12-fa1ad5752374
ms.openlocfilehash: 6eba93562d4c6a8ffa4150453deed88844d4e297
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695132"
---
# <a name="return-or-skip-elements-in-a-sequence"></a>Elementos Return ou Skip em uma sequência

Use o operador <xref:System.Linq.Queryable.Take%2A> para retornar um número específico de elementos em uma sequência e ignorar o restante.  
  
 Use o operador <xref:System.Linq.Queryable.Skip%2A> para ignorar um número específico de elementos em uma sequência e retornar o restante.  
  
> [!NOTE]
> <xref:System.Linq.Enumerable.Take%2A> e <xref:System.Linq.Enumerable.Skip%2A> possuem certas limitações quando são usados em consultas no SQL Server 2000. Para obter mais informações, consulte a entrada "ignorar e considerar exceções no SQL Server 2000" em [solução de problemas](troubleshooting.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] traduz <xref:System.Linq.Queryable.Skip%2A> usando uma subconsulta com a `NOT EXISTS` cláusula SQL. Essa conversão apresenta as seguintes limitações:  
  
- O argumento deve ser um conjunto. Não há suporte para vários conjuntos, mesmo se ordenados.  
  
- A consulta gerada pode ser muito mais complexa do que a consulta gerada para a consulta base em que <xref:System.Linq.Queryable.Skip%2A> é aplicado. Essa complexidade pode reduzir o desempenho ou até mesmo causar um tempo limite.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa `Take` para selecionar os primeiros cinco `Employees` contratados. Observe que a coleção é classificada primeiro por `HireDate`.  
  
 [!code-csharp[DLinqQueryExamples#16](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#16)]
 [!code-vb[DLinqQueryExamples#16](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#16)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa <xref:System.Linq.Queryable.Skip%2A> para selecionar todos, exceto os 10 `Products` mais caros.  
  
 [!code-csharp[DLinqQueryExamples#17](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#17)]
 [!code-vb[DLinqQueryExamples#17](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#17)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir combina os métodos <xref:System.Linq.Queryable.Skip%2A> e <xref:System.Linq.Queryable.Take%2A> para ignorar os primeiros 50 registros e retornar os 10 seguintes.  
  
 [!code-csharp[DLinqQueryExamples#18](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#18)]
 [!code-vb[DLinqQueryExamples#18](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#18)]  
  
 As operações <xref:System.Linq.Queryable.Take%2A> e <xref:System.Linq.Queryable.Skip%2A> são bem definidas somente em conjuntos ordenados. A semântica de conjuntos não ordenados ou de vários conjuntos é indefinida.  
  
 Devido às limitações de ordenamento no SQL, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tenta mover a ordenação do argumento do operador <xref:System.Linq.Queryable.Take%2A> ou <xref:System.Linq.Queryable.Skip%2A> para o resultado do operador.  
  
> [!NOTE]
> A tradução é diferente para SQL Server 2000 e SQL Server 2005. Se você planeja usar <xref:System.Linq.Queryable.Skip%2A> o com uma consulta de qualquer complexidade, use SQL Server 2005.  
  
 Considere a seguinte [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] consulta para SQL Server 2000:  
  
 [!code-csharp[DLinqQueryExamples#19](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#19)]
 [!code-vb[DLinqQueryExamples#19](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#19)]  
  
 O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] move a ordenação para o final do código SQL, da seguinte maneira:  
  
```sql
SELECT TOP 1 [t0].[CustomerID], [t0].[CompanyName],  
FROM [Customers] AS [t0]  
WHERE (NOT (EXISTS(  
    SELECT NULL AS [EMPTY]  
    FROM (  
        SELECT TOP 1 [t1].[CustomerID]  
        FROM [Customers] AS [t1]  
        WHERE [t1].[City] = @p0  
        ORDER BY [t1].[CustomerID]  
        ) AS [t2]  
    WHERE [t0].[CustomerID] = [t2].[CustomerID]  
    ))) AND ([t0].[City] = @p1)  
ORDER BY [t0].[CustomerID]  
```  
  
 Quando <xref:System.Linq.Queryable.Take%2A> e <xref:System.Linq.Queryable.Skip%2A> são encadeados juntos, toda a ordenação especificada deve ser consistente. Caso contrário, os resultados serão indefinidos.  
  
 Para argumentos integrais constantes e não negativos, baseados na especificação SQL, <xref:System.Linq.Queryable.Take%2A> e <xref:System.Linq.Queryable.Skip%2A> são bem definidos.  
  
## <a name="see-also"></a>Consulte também

- [Exemplos de consulta](query-examples.md)
- [Conversão padrão de operador de consulta](standard-query-operator-translation.md)
