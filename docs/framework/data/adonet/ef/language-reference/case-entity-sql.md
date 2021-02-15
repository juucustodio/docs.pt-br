---
description: 'Saiba mais sobre: CASE (Entity SQL)'
title: CASO (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 26a47873-e87d-4ba2-9e2c-3787c21efe89
ms.openlocfilehash: 58f51aa46f41c3b502bcd6d364e893a12624f4cf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739489"
---
# <a name="case-entity-sql"></a>CASO (Entity SQL)

Avalia um conjunto de expressões de `Boolean` para determinar o resultado.  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp  
CASE  
     WHEN Boolean_expression THEN result_expression
    [ ...n ]
     [
    ELSE else_result_expression
     ]
END  
```  
  
## <a name="arguments"></a>Argumentos  

 `n`  
 É um espaço reservado que indica que várias QUANDO as cláusulas de `Boolean_expression` ENTÃO `result_expression` podem ser usadas.  
  
 ENTÃO `result_expression`  
 A expressão é retornada quando `Boolean_expression` avalia a `true`. `result expression` é qualquer expressão válida.  
  
 `else_result_expression`OUTRO  
 A expressão é retornada se qualquer operação de comparação avalia a `true`. Se esse argumento é omitido e nenhuma operação de comparação avalia a `true`, os CASOS retornam o zero. `else_result_expression` é qualquer expressão válida. Os tipos de dados de `else_result_expression` e qualquer `result_expression` devem ser os mesmos ou devem ser uma conversão implícita.  
  
 QUANDO `Boolean_expression`  
 A expressão é avaliada de `Boolean` quando o formato pesquisada de CASOS é usado. `Boolean_expression` é qualquer expressão válida de `Boolean` .  
  
## <a name="return-value"></a>Valor retornado  

 Retorna o tipo mais alto de precedência de conjunto de tipos em `result_expression` e `else_result_expression`opcional.  
  
## <a name="remarks"></a>Comentários  

 A [!INCLUDE[esql](../../../../../../includes/esql-md.md)] expressão CASE é semelhante à expressão de caso Transact-SQL. Você usa a expressão dos casos para fazer uma série de teste condicional para determinar qual expressão renderá o resultado apropriado. Este formulário da expressão dos casos se aplica a uma série de uma ou mais expressões de `Boolean` para determinar a expressão resultante correta.  
  
 A função de CASOS avaliar `Boolean_expression` para o QUANDO cada cláusula na ordem especificada, e retornar `result_expression` de primeiro `Boolean_expression` que avalia para `true`. As expressões restantes não são avaliadas. Se nenhum `Boolean_expression` avalia a `true`, o mecanismo de base de dados retorna `else_result_expression` se uma cláusula OUTRA for especificada, ou um valor nulo se nenhuma cláusula OUTRA é especificado.  
  
 Uma declaração de CASOS não pode retornar um multiset.  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity usa a expressão de CASOS para avaliar um conjunto de expressões de `Boolean` para determinar o resultado. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna os resultados de primitivatype](../how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecutePrimitiveTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#CASE_WHEN_THEN_ELSE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#case_when_then_else)]  
  
## <a name="see-also"></a>Consulte também

- [THEN](then-entity-sql.md)
- [SELECT](select-entity-sql.md)
- [Referência de Entity SQL](entity-sql-reference.md)
