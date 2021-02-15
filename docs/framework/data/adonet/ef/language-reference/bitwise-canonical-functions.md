---
description: 'Saiba mais sobre: funções canônicas de bits'
title: Funções canônicas bit a bit
ms.date: 03/30/2017
ms.assetid: 993868ca-16e3-47b6-9915-c29cd63b0a21
ms.openlocfilehash: a811c707749af2d2fa9472ae2d1444c3f076aeec
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99697095"
---
# <a name="bitwise-canonical-functions"></a>Funções canônicas bit a bit

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] inclui funções canônicas bit a bit.  
  
## <a name="remarks"></a>Comentários  

 A tabela a seguir mostra a [!INCLUDE[esql](../../../../../../includes/esql-md.md)] bit a bit funções canônicas. Essas funções retornarão `Null` se a `Null` entrada for fornecida. O tipo de retorno de funções é o mesmo que os tipos de argumento. Os argumentos devem ser do mesmo tipo, se a função recebe mais de um argumento. Para executar operações bit a bit por tipos diferentes, você precisará converter explicitamente o mesmo tipo.  
  
|Função|Descrição|  
|--------------|-----------------|  
|`BitWiseAnd (` `value1` `,`  `value2` `)`|Retorna a conjução bit a bit de `value1` e de `value2` como o tipo de `value1` e de `value2`.<br /><br /> **Argumentos**<br /><br /> A `Byte` , `Int16` , e `Int32` `Int64` .<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 1.`<br /><br /> `BitWiseAnd(1,3)`|  
|`BitWiseNot (` `value` `)`|Retorna a negação bit a bit de `value`.<br /><br /> **Argumentos**<br /><br /> A `Byte` , `Int16` , e `Int32` `Int64` .<br /><br /> **Exemplo**<br /><br /> `-- The following example returns -4.`<br /><br /> `BitWiseNot(3)`|  
|`BitWiseOr (` `value1` `,`  `value2` `)`|Retorna a disjução bit a bit de `value1` e de `value2` como o tipo de `value1` e de `value2`.<br /><br /> **Argumentos**<br /><br /> A `Byte` , `Int16` , `Int32` e `Int64` .<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 3.`<br /><br /> `BitWiseOr(1,3)`|  
|`BitWiseXor (` `value1` `,`  `value2` `)`|Retorna a disjunção bit a bit exclusiva de `value1` e de `value2` como o tipo de `value1` e de `value2`.<br /><br /> **Argumentos**<br /><br /> A `Byte` , `Int16` , `Int32` e `Int64` .<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 2.`<br /><br /> `BitWiseXor (1,3)`|  
  
## <a name="see-also"></a>Consulte também

- [Funções canônicas](canonical-functions.md)
