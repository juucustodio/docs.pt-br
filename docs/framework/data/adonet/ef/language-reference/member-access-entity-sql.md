---
description: Saiba mais sobre:. (Acesso de membro) (Entity SQL)
title: . (Acesso de membro) (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 4733e3b2-3efa-4b96-b591-ac31350e96ad
ms.openlocfilehash: 94833d3525c7d17cadaef15065b3dcbdb43a6ded
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739372"
---
# <a name="-member-access-entity-sql"></a>. (Acesso de membro) (Entity SQL)

O operador de ponto (.) é o [!INCLUDE[esql](../../../../../../includes/esql-md.md)] operador de acesso de membro. Você usa o operador de acesso de membro para produzir o valor de uma propriedade ou um campo de uma instância do tipo estrutural de modelo conceitual.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
expression.identifier  
```  
  
## <a name="arguments"></a>Argumentos  

 `expression`  
 Uma instância de um tipo estrutural de modelo conceitual.  
  
 `identifier`  
 Uma propriedade ou um campo que pertençam a uma instância do objeto.  
  
## <a name="remarks"></a>Comentários  

 O operador ponto (.) pode ser usado para extrair campos de um registro, semelhante a extrair propriedades de um complexo ou tipo de objeto. Por exemplo, se n do tipo name for um membro do tipo Person, e p for uma instância do tipo Person, p. n será uma expressão de acesso de membro legal que produz um valor do tipo Name.  
  
 `select p.Name.FirstName from LOB.Person as p`  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
