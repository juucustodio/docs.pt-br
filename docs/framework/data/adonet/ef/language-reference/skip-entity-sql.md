---
description: 'Saiba mais sobre: SKIP (Entity SQL)'
title: IGNORAR (Entity SQL)
ms.date: 03/30/2017
ms.assetid: e2139412-8ea4-451b-8f10-91af18dfa3ec
ms.openlocfilehash: f4924acae6e351e076b5795cf47d63966ebdcb43
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99768006"
---
# <a name="skip-entity-sql"></a>IGNORAR (Entity SQL)

Você pode executar a físico paginação usando a cláusula subpropriedades de SKIP na cláusula GROUP BY. A SKIP não pode ser usada separada de cláusula GROUP BY.

## <a name="syntax"></a>Sintaxe

```sql
[ SKIP n ]
```

## <a name="arguments"></a>Argumentos

`n` \
O número de itens para ignorar.

## <a name="remarks"></a>Comentários

Se uma subpropriedades cláusula de expressão de SKIP está presente em uma cláusula GROUP BY, os resultados que serão classificados concordam a especificação do tipo e o conjunto de resultados incluirá as linhas a partir da linha seguinte logo após a expressão de SKIP. Por exemplo, a SKIP 5 ignorará as primeiras cinco linhas e retornará a sexta linha avançar.

> [!NOTE]
> Uma consulta de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não é válido se o modificador TOP e a subpropriedades cláusula de SKIP estiverem presentes na mesma expressão de consulta. A consulta deve ser reescrita alterando a expressão TOP para a expressão de LIMIT.

> [!NOTE]
> No SQL Server 2000, usar SKIP com ORDER BY em colunas não chave pode retornar resultados incorretos. Mais do que o número de linhas especificado podem ser ignoradas se a coluna de chave não tem dados duplicados nele. Isso ocorre devido a como o SKIP é convertido para SQL Server 2000. Por exemplo, o seguinte código mais de cinco linhas podem ser ignoradas se `E.NonKeyColumn` tem valores duplicados:
>
> ```sql
> SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L
> ```

A [!INCLUDE[esql](../../../../../../includes/esql-md.md)] consulta em [como: paginar os resultados da consulta](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100)) usa o operador order by com Skip para especificar a ordem de classificação usada nos objetos retornados em uma instrução SELECT.

## <a name="see-also"></a>Consulte também

- [ORDER BY](order-by-entity-sql.md)
- [Como: paginar os resultados da consulta](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))
- [Houver](paging-entity-sql.md)
- [INÍCIO](top-entity-sql.md)
