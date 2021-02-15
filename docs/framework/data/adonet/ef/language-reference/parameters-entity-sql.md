---
description: 'Saiba mais sobre: parâmetros (Entity SQL)'
title: Parâmetros (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 8d618edd-0988-4ff2-8263-ce59448af7a5
ms.openlocfilehash: 77b1e6ee95b5d367fec8d99345bbb416c2b9787d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724525"
---
# <a name="parameters-entity-sql"></a>Parâmetros (Entity SQL)

Os parâmetros são variáveis que são definidos fora de [!INCLUDE[esql](../../../../../../includes/esql-md.md)], geralmente através de uma associação API que é usada por uma linguagem de host. Cada parâmetro tem um nome e um tipo. Os nomes de parâmetro são definidos em expressões de consulta com o símbolo arroba (@) como um prefixo. Isso os desambigua dos nomes das propriedades ou de outros nomes definidos na consulta.  
  
 O host linguagem que associa API fornece APIs para parâmetros de associação.  
  
## <a name="example"></a>Exemplo  
  
```sql  
SELECT c
      FROM LOB.Customers AS c
      WHERE c.Name = @name  
```  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Visão geral da Entity SQL](entity-sql-overview.md)
