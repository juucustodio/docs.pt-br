---
description: 'Saiba mais sobre: IN (Entity SQL)'
title: IN (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 51662950-ee01-4857-b7b9-311dd8515966
ms.openlocfilehash: 234ed15430e44d12d4ca7c98fcb4a7bc03d117f9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99748590"
---
# <a name="in-entity-sql"></a>IN (Entity SQL)

Determina se um valor corresponde a qualquer valor em uma coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
value [ NOT ] IN expression  
```  
  
## <a name="arguments"></a>Argumentos  

 `value`  
 Qualquer expressão válida que retorna o valor para corresponder.  
  
 [ NOT ]  
 Especifica que o resultado `Boolean` de IN seja negado.  
  
 `expression`  
 Qualquer expressão válida que retorna a coleção para testar uma correspondência. Todas as expressões devem ser do mesmo tipo ou de uma base comum ou um tipo derivado que `value`.  
  
## <a name="return-value"></a>Valor retornado  

 `true` se o valor for encontrado na coleção; nulo se o valor for nulo ou a coleção for nula; caso contrário, `false`. Usar NOT IN nega os resultados de IN.  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta de Entity SQL usa o operador IN para determinar se um valor corresponde a qualquer valor em uma coleção. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#IN](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#in)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
