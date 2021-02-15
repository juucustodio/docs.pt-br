---
description: Saiba mais sobre:/(divisão) (Entity SQL)
title: '- Dividir (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: ef48c368-f3ed-4275-8ada-4e9649781262
ms.openlocfilehash: 4ac487c636c460401eeb147dc7ce1a8d8ba7f7ad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724629"
---
# <a name="-divide-entity-sql"></a>/ (Divisão) (Entity SQL)

Divide um número por outro.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
dividend / divisor  
```  
  
## <a name="arguments"></a>Argumentos  

 `dividend`  
 A expressão numérica a divisão. `dividend` é qualquer expressão válida de ambos os tipos de dados numéricos.  
  
 `divisor`  
 A expressão numérica para dividir pelo dividendo. `divisor` é qualquer expressão válida de ambos os tipos de dados numéricos.  
  
## <a name="result-types"></a>Tipos de resultado  

 O tipo de dados que resulta da promoção de tipos implícito dos dois argumentos. Para obter mais informações sobre a promoção de tipos implícitas, consulte [sistema de tipos](type-system-entity-sql.md).  
  
## <a name="example"></a>Exemplo  

 A consulta Entity SQL a seguir usa o operador/aritmética para dividir um número por outro. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:  
  
1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:  
  
 [!code-sql[DP EntityServices Concepts#DIVIDE](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#divide)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
