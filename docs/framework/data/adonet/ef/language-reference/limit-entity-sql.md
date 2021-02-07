---
description: 'Saiba mais sobre: LIMIT (Entity SQL)'
title: LIMITAR (Entity SQL)
ms.date: 03/30/2017
ms.assetid: c22ffede-0a52-44d1-99b9-4a91e651e1b9
ms.openlocfilehash: 873f3fd5ed83d04313aff92bf1f97e07001c3f08
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99748200"
---
# <a name="limit-entity-sql"></a>LIMITAR (Entity SQL)

A paginação física pode ser executada usando a subcláusula LIMIT em uma ORDER BY. LIMIT não pode ser usada separadamente da cláusula ORDER BY.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
[ LIMIT n ]  
```  
  
## <a name="arguments"></a>Argumentos  

 `n`  
 O número de itens que serão selecionados.  
  
 Se uma subcláusula de expressão LIMIT estiver presente em uma cláusula ORDER BY, a consulta será classificada de acordo com a especificação de classificação e o número de linhas resultante será restrito pela expressão LIMIT. Por exemplo, LIMIT 5 restringirá o conjunto de resultados a 5 instâncias ou linhas. LIMIT é funcionalmente equivalente à TOP com a exceção de que a LIMIT requer que a cláusula ORDER BY esteja presente. SKIP e LIMIT podem ser usadas independentemente junto com a cláusula ORDER BY.  
  
> [!NOTE]
> Uma consulta Entity SQL será considerada inválida se o modificador TOP e a subcláusula SKIP estiverem presentes na mesma expressão de consulta. A consulta deve ser reescrita alterando a expressão TOP para uma expressão LIMIT.  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta Entity SQL usa o operador ORDER BY com LIMIT para especificar ordem de classificação usada em objetos retornados em uma instrução SELECT. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#LIMIT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#limit)]  
  
## <a name="see-also"></a>Consulte também

- [ORDER BY](order-by-entity-sql.md)
- [Como: paginar os resultados da consulta](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))
- [Houver](paging-entity-sql.md)
- [INÍCIO](top-entity-sql.md)
