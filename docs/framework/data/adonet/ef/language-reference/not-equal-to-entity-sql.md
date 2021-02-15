---
description: Saiba mais sobre:! = (diferente de) (Entity SQL)
title: '!= (Não é igual a) (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: 3b4a02ad-ddfc-4c42-8dfa-676234461312
ms.openlocfilehash: a7a96606fb1834b757253948c3a0d2cde11893dc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696393"
---
# <a name="-not-equal-to-entity-sql"></a>!= (Não é igual a) (Entity SQL)

Compara duas expressões para determinar se a expressão da esquerda não é igual a expressão da direita. O operador! = (diferente de) é funcionalmente equivalente ao operador de <> .  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
expression != expression  
-- or  
expression <> expression  
```  
  
## <a name="arguments"></a>Argumentos  

 `expression`  
 Qualquer expressão válida. Ambas as expressões devem ter tipos de dados implicitamente conversíveis.  
  
## <a name="result-types"></a>Tipos de resultado  

 `true` se a expressão da esquerda não for igual à expressão da direita; caso contrário, `false`.  
  
## <a name="example"></a>Exemplo  

 A consulta do Entity SQL usa o operador != para comparar duas expressões para determinar se a expressão da esquerda não é igual à expressão da direita. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#NOT_EQUALS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#not_equals)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
