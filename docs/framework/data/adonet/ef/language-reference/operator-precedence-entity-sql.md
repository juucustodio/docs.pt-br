---
description: 'Saiba mais sobre: precedência de operador (Entity SQL)'
title: Precedência do operador (Entity SQL)
ms.date: 03/30/2017
ms.assetid: e92e4ca5-2889-4266-9625-47f0eb01a948
ms.openlocfilehash: 72cfdecf7dfe4ce590d99e866429e771f9ede231
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739320"
---
# <a name="operator-precedence-entity-sql"></a>Precedência do operador (Entity SQL)

Quando uma [!INCLUDE[esql](../../../../../../includes/esql-md.md)] consulta tem vários operadores, a precedência de operador determina a sequência na qual as operações são executadas. A ordem de execução pode impactar significativamente no resultado da consulta.  
  
 Os níveis de precedência dos operadores são mostrados na tabela a seguir. Um operador com um nível mais alto é avaliada antes de um operador com um nível inferior.  
  
|Level|Tipo de operação|Operador|  
|-----------|--------------------|--------------|  
|1|Primário|`. , [] ()`|  
|2|Unário|`! not`|  
|3|Multiplicativo|`* / %`|  
|4|Aditiva|`+ -`|  
|5|Ordenando|`< > <= >=`|  
|6|Igualitário|`= != <>`|  
|7|AND condicional|`and &&`|  
|8|OR condicional|`or &#124;&#124;`|  
  
 Quando dois operadores em uma expressão têm o mesmo nível de precedência de operadores, são avaliados esquerda para a direita, com base na sua posição na consulta. Por exemplo, `x+y-z` é avaliado como `(x+y)-z`.  
  
 Você pode usar parênteses para substituir a precedência de operadores definida em uma consulta. Todos dentro dos parênteses é avaliado primeiro para produzir um único resultado antes que o resultado pode ser usado por qualquer operador fora dos parênteses. Por exemplo, `x+y*z` multiplica `y` por `z` e, em seguida `x` , adiciona, mas `(x+y)*z` adiciona `x` `y` e, em seguida, multiplica o resultado por `z` .  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
