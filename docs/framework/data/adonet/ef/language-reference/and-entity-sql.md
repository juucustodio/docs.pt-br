---
description: 'Saiba mais sobre: &amp; &amp; (e) (Entity SQL)'
title: '&amp;&amp; E (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: e7d24213-471d-4807-b85e-570375df89b5
ms.openlocfilehash: 14fc6bc3f58ac78cb9806a7f421db87bbad048ae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99697173"
---
# <a name="ampamp-and-entity-sql"></a>&amp;&amp; E (Entity SQL)

Retorna `true` se as duas expressões são `true`; caso contrário, `false` ou `NULL`.  
  
## <a name="syntax"></a>Syntax  
  
```csharp  
boolean_expression AND boolean_expression
```

ou  

```csharp
boolean_expression && boolean_expression  
```  
  
## <a name="arguments"></a>Argumentos  

 `boolean_expression`  
 Qualquer expressão válida que retorna um valor booleano.  
  
## <a name="remarks"></a>Comentários  

 O e comercial duplo (&&) têm a mesma funcionalidade que o operador AND.  
  
 A tabela a seguir mostra valores e tipos de retorno de entrada possíveis.  
  
||`TRUE`|`FALSE`|`NULL`|  
|-|------------|-------------|------------|  
|`TRUE`|TRUE|FALSE|NULO|  
|`FALSE`|FALSE|FALSE|FALSE|  
|`NULL`|NULO|FALSE|NULO|  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity demonstra como usar o operador AND. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#AND](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#and)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
