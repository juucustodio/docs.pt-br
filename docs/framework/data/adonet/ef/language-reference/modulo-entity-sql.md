---
description: 'Saiba mais sobre: (módulo) (Entity SQL)'
title: (Módulo) (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 243ddc4f-3c4e-41e1-a3ef-4ed39e36248b
ms.openlocfilehash: 8ac9bf2fa9dbee843215dcfeed13fefc7bd54796
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696627"
---
# <a name="modulo-entity-sql"></a>(Módulo) (Entity SQL)

Retorna o resto de uma expressão dividida por outra.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
dividend % divisor  
```  
  
## <a name="arguments"></a>Argumentos  

 `dividend`  
 A expressão numérica a divisão. `dividend` é qualquer expressão válida de ambos os tipos de dados numéricos.  
  
 `divisor`  
 A expressão numérica para dividir pelo dividendo. `divisor` é qualquer expressão válida de ambos os tipos de dados numéricos.  
  
## <a name="result-types"></a>Tipos de resultado  

 Edm.Int32  
  
## <a name="example"></a>Exemplo  

 A seguinte consulta SQL Entity usa os % do operador aritmético para retornar o restante de uma expressão dividida por outra. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#MODULO](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#modulo)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
