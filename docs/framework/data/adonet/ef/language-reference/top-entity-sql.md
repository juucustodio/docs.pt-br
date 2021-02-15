---
description: 'Saiba mais sobre: TOP (Entity SQL)'
title: TOPO (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 4a4a0954-82e2-4eae-bcaf-7c4552f3532d
ms.openlocfilehash: 51e4ce53cff4b47f6f57b6b856ccb09b38e639cf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99673434"
---
# <a name="top-entity-sql"></a>TOPO (Entity SQL)

A cláusula SELECT pode ter uma cláusula as subjanelas TOP opcional após o modificador opcional de ALL/DISTINCT. A cláusula subpropriedades TOP especifica que apenas definir primeiro as linhas será retornado do resultado da consulta.

## <a name="syntax"></a>Sintaxe

```sql
[ TOP (n) ]
```

## <a name="arguments"></a>Argumentos

`n` A expressão numérica que especifica o número de linhas a serem retornadas. `n` pode ser um único literal numérico ou um único parâmetro.

## <a name="remarks"></a>Comentários

A expressão TOP deve ser um único literal numérico ou um único parâmetro. Se um literal constante é usado, o tipo literal deve ser implicitamente promotable a Edm.Int64 (byte, int16 ou int32, int64 ou qualquer tipo de provedor que o mapeamento para um tipo que é promotable a Edm.Int64) e seu valor deve ser maior ou igual a zero. Se não uma exceção será lançada. Se um parâmetro é usado como uma expressão, o tipo de parâmetro deve também ser implicitamente promotable a Edm.Int64, mas não haverá validação do valor do parâmetro real durante a compilação porque valores de parâmetro são delimitados tarde.

A seguir está um exemplo da expressão de TOP da constante:

```sql
select distinct top(10) c.a1, c.a2 from T as a
```

Veja a seguir um exemplo de expressão superior parametrizada:

```sql
select distinct top(@topParam) c.a1, c.a2 from T as a
```

A TOP é não determinística a menos que a consulta é classificada. Se você precisar de um resultado determinístico, use as subcláusulas [Skip](skip-entity-sql.md) e [Limit](limit-entity-sql.md) na cláusula [order by](order-by-entity-sql.md) . A TOP e os SKIP/LIMIT são mutuamente exclusivos.

## <a name="example"></a>Exemplo

A seguinte consulta de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usa a TOP para especificar a uma linha superior a ser retornado do resultado da consulta. A consulta é baseada no modelo de vendas AdventureWorks. Para compilar e executar essa consulta, siga estas etapas:

1. Siga o procedimento em [como executar uma consulta que retorna resultados de estruturaistype](../how-to-execute-a-query-that-returns-structuraltype-results.md).

2. Passe a consulta a seguir como um argumento para o método `ExecuteStructuralTypeQuery`:

    [!code-sql[DP EntityServices Concepts#TOP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#top)]

## <a name="see-also"></a>Consulte também

- [SELECT](select-entity-sql.md)
- [SALTAR](skip-entity-sql.md)
- [LIMITE](limit-entity-sql.md)
- [ORDER BY](order-by-entity-sql.md)
- [Referência de Entity SQL](entity-sql-reference.md)
