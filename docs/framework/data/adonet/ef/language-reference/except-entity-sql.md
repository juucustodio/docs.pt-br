---
description: 'Saiba mais sobre: EXCEPT (Entity SQL)'
title: EXCETO (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 69cc23e5-3f8f-4b49-b20e-2f84ff11c80d
ms.openlocfilehash: fd66d8dc6e22a73afbfd27e6eb1fd6c8bb9d3475
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786388"
---
# <a name="except-entity-sql"></a>EXCETO (Entity SQL)

Retorna uma coleção de todos os valores distintos da expressão de consulta para a esquerda do operando EXCEPT que também não são retornados da expressão de consulta à direita do operando EXCEPT. Todas as expressões devem ser do mesmo tipo ou de uma base comum ou um tipo derivado que `expression`.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
expression EXCEPT expression  
```  
  
## <a name="arguments"></a>Argumentos  

 `expression`  
 Qualquer expressão de consulta válida que retornar uma coleção para comparar com a coleção retornada de outra expressão de consulta.  
  
## <a name="return-value"></a>Valor retornado  

 Uma coleção de mesmos tipos ou uma base comum ou um tipo derivado como `expression`.  
  
## <a name="remarks"></a>Comentários  

 EXCETO é um dos operadores definidos [!INCLUDE[esql](../../../../../../includes/esql-md.md)] . Todos os operadores definidos [!INCLUDE[esql](../../../../../../includes/esql-md.md)] são avaliados da esquerda para a direita. A tabela a seguir mostra a precedência de operadores definidos [!INCLUDE[esql](../../../../../../includes/esql-md.md)] .  
  
|Precedência|Operadores|  
|----------------|---------------|  
|O mais alto|INTERSECT|  
||UNION<br /><br /> TODOS UNION|  
||EXCEPT|  
|O menor|EXISTS<br /><br /> OVERLAPS<br /><br /> FLATTEN<br /><br /> SET|  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity usa A QUE operador NOT SER para retornar uma coleção de todos os valores diferentes de duas expressões de consulta. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#EXCEPT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#except)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
