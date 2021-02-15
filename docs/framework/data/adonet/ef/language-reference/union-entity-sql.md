---
description: 'Saiba mais sobre: UNION (Entity SQL)'
title: UNIÃO (Entity SQL)
ms.date: 03/30/2017
ms.assetid: df98a4db-b00d-4c8b-bd74-0d285f27e1df
ms.openlocfilehash: f02b3d76d8c21848b7a1b7ef5e7bbf749aea5c0f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99673304"
---
# <a name="union-entity-sql"></a>UNIÃO (Entity SQL)

Combina os resultados de duas ou mais consultas em uma única coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
expression  
UNION [ ALL ]  
expression  
```  
  
## <a name="arguments"></a>Argumentos  

 `expression`  
 Qualquer expressão de consulta válida que retorna uma coleção para combinar com a coleção todas as expressões deve ser do mesmo tipo ou de uma base comum ou um tipo derivado que `expression`.  
  
 UNION  
 Especifica que as várias coleções devem ser combinadas e retornado como uma única coleção.  
  
 ALL  
 Especifica que as várias coleções devem ser combinadas e retornado como uma única coleção, incluir duplica. Se não especificado, as duplicatas são removidas da coleção de resultado.  
  
## <a name="return-value"></a>Valor retornado  

 Uma coleção de mesmos tipos ou uma base comum ou um tipo derivado como `expression`.  
  
## <a name="remarks"></a>Comentários  

 UNION é um dos operadores definidos [!INCLUDE[esql](../../../../../../includes/esql-md.md)] . Todos os operadores definidos [!INCLUDE[esql](../../../../../../includes/esql-md.md)] são avaliados da esquerda para a direita. Para obter informações de precedência para os [!INCLUDE[esql](../../../../../../includes/esql-md.md)] operadores de conjunto, consulte [Except](except-entity-sql.md).  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity usa o UNION ALL operador para combinar os resultados das duas consultas em uma única coleção. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#UNION](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#union)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
