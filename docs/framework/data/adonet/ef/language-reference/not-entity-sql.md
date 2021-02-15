---
description: Saiba mais sobre:! (NÃO) (Entity SQL)
title: '! (NÃO) (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: a1447a34-df06-4393-93c3-0612ebd41abc
ms.openlocfilehash: 648cc4ff73769ae280570b2d42934b2001fa5182
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696445"
---
# <a name="-not-entity-sql"></a>! (NÃO) (Entity SQL)

Nega uma expressão de `Boolean` .  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
NOT boolean_expression  
-- or  
! boolean_expression  
```
  
## <a name="arguments"></a>Argumentos  

 `boolean_expression`  
 Qualquer expressão válida que retorna um valor booleano.  
  
## <a name="remarks"></a>Comentários  

 O ponto de exclamação (!) tem a mesma funcionalidade que o operador NOT.  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity usa o operador NOT nega uma expressão de `Boolean` . A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#NOT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#not)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
