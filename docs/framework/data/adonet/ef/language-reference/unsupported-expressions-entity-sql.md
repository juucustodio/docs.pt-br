---
description: 'Saiba mais sobre: expressões sem suporte'
title: Expressões sem suporte (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5e79da7e-e78a-413c-8fb0-f3f9cd84f579
dev_langs:
- sql
ms.openlocfilehash: ceb57dc78f9685a79de987d15f7fd57a583b75a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99673291"
---
# <a name="unsupported-expressions"></a>Expressões sem suporte

Este tópico descreve as expressões Transact-SQL que não têm suporte no [!INCLUDE[esql](../../../../../../includes/esql-md.md)] . Para obter mais informações, consulte [como Entity SQL difere do Transact-SQL](how-entity-sql-differs-from-transact-sql.md).

## <a name="quantified-predicates"></a>Predicados quantificados

O Transact-SQL permite constructos da seguinte forma:

```sql
sal > all (select salary from employees)
sal > any (select salary from employees)
```

[!INCLUDE[esql](../../../../../../includes/esql-md.md)], no entanto, não suporta como compilações. As expressões equivalentes podem ser gravadas em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] como segue:

```sql
not exists(select 0 from employees as e where sal <= e.salary)
exists(select 0 from employees as e where sal > e.salary)
```

## <a name="-operator"></a>Operador *

O Transact-SQL dá suporte ao uso do operador * na cláusula SELECT para indicar que todas as colunas devem ser projetadas. Não há suporte para isso no [!INCLUDE[esql](../../../../../../includes/esql-md.md)] .

## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
- [Como o Entity SQL difere do Transact-SQL](how-entity-sql-differs-from-transact-sql.md)
