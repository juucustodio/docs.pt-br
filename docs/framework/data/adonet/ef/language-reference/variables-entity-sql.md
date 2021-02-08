---
description: 'Saiba mais sobre: variáveis (Entity SQL)'
title: Variáveis (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 3eed222a-f8f6-46b6-9cd5-220cc0e4e5d8
ms.openlocfilehash: 134fee8f61c8e87a18520e6622f6a6a5cceb0076
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795034"
---
# <a name="variables-entity-sql"></a>Variáveis (Entity SQL)

## <a name="variable"></a>Variável  

 Uma expressão variável é uma referência a uma expressão chamado definida no escopo atual. Uma referência de variável deve ser um [!INCLUDE[esql](../../../../../../includes/esql-md.md)] identificador válido, conforme definido em [identificadores](identifiers-entity-sql.md).  
  
 O exemplo a seguir mostra o uso de uma variável na expressão. `c` na cláusula é a definição da variável. O uso de `c` na cláusula SELECT representa a referência variável.  
  
```sql  
select c
from LOB.customers as c  
```  
  
## <a name="see-also"></a>Consulte também

- [Identificadores](identifiers-entity-sql.md)
- [Parâmetros](parameters-entity-sql.md)
- [Visão geral da Entity SQL](entity-sql-overview.md)
