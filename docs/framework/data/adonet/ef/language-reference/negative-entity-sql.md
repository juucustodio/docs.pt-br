---
description: Saiba mais sobre:-(negativo) (Entity SQL)
title: '- Seriamente (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: 208e54ef-4741-4ec5-89d6-6ff700863cb0
ms.openlocfilehash: f3d30ce36b95e44755d148dc06279f67f15b0664
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712877"
---
# <a name="--negative-entity-sql"></a>- (Negativo) (Entity SQL)

Retorna o negativo o valor de uma expressão numérica.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
- expression  
```  
  
## <a name="arguments"></a>Argumentos  

 `expression`  
 Qualquer expressão válida de qualquer dos tipos de dados numéricos.  
  
## <a name="result-types"></a>Tipos de resultado  

 O tipo de dados de `expression`.  
  
## <a name="remarks"></a>Comentários  

 Se `expression` é um tipo sem sinal, o tipo do resultado será o tipo com sinal que relaciona o melhor para o tipo de `expression`. Por exemplo, se `expression` é de bytes de tipo, um valor do tipo Int16 será retornado.  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity usa o operador - aritmético para retornar o negativo o valor de uma expressão numérica. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#NEGATIVE](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#negative)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
