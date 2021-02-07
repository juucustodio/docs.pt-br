---
description: 'Saiba mais sobre: definições de tipo (Entity SQL)'
title: Definições de tipo (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 306b204a-ade5-47ef-95b5-c785d2da4a7e
ms.openlocfilehash: e5a66ed9ea456733bab9c68d96ef5c176dad5651
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99673408"
---
# <a name="type-definitions-entity-sql"></a>Definições de tipo (Entity SQL)

Uma definição de tipo é usada na instrução de declaração de uma função in-line de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] .  
  
## <a name="remarks"></a>Comentários  

 A instrução de declaração para uma função embutida consiste na palavra-chave [Function](function-entity-sql.md) seguida pelo identificador que representa o nome da função (por exemplo, "MyAvg") seguido por uma lista de definições de parâmetro entre parênteses (por exemplo, "coleção indevido (Decimal)").  
  
 A lista de definição de parâmetro consiste de zero ou mais definições de parâmetro. Cada definição de parâmetro consiste em um identificador (o nome do parâmetro para a função, por exemplo, a dívidas “”) seguido por uma definição de tipo (por exemplo, “coleção (decimal) ").  
  
 Definições de tipo podem ser qualquer:  
  
- O tipo identificador (por exemplo, “Int32” ou “AdventureWorks.Order”).  
  
- A palavra-chave `COLLECTION` seguido por outra definição de tipo no parêntese (por exemplo, “coleção (AdventureWorks.Order) ").  
  
- A LINHA seguida por uma lista de definições de propriedade no parêntese (por exemplo, “linha de palavras-chave (x) AdventureWorks.Order "). As definições de propriedade têm um formato como " `identifier type_definition` , `identifier type_definition` ,...".  
  
- A referência seguido pelo tipo identificador no parêntese (por exemplo, “referência de palavras-chave (AdventureWorks.Order) "). O operador de definição de tipo de referência requer um tipo de entidade como o argumento. Você não pode especificar um tipo primitivo como o argumento.  
  
 Você também pode aninhar definições de tipo (por exemplo, “coleção (linha (referência de AdventureWorks.Order (x))").  
  
 As opções de definição de tipo são:  
  
- `IdentifierName supported_type`, ou  
  
- COLEÇÃO de`IdentifierName` (`type_definition`), ou  
  
- LINHA de`IdentifierName` (`property_definition`), ou  
  
- referência de`IdentifierName` (`supported_entity_type`)  
  
 A opção de definição de propriedade é `IdentifierName type_definition`.  
  
 Os tipos suportados são alguns tipos no namespace atual. Esses incluem a primitiva e os tipos de entidade.  
  
 Os tipos de entidade suporte a apenas tipos de entidade no namespace atual. Não incluem tipos primitivos.  
  
## <a name="examples"></a>Exemplos  

 A seguir está um exemplo de uma definição de tipo simples.  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 EDM.Decimal) AS (  
   Round(p1)  
)  
MyRound(CAST(1.7 as EDM.Decimal))  
```  
  
 A seguir está um exemplo de uma definição de tipo de COLEÇÃO.  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Collection(EDM.Decimal)) AS (  
   Select Round(p1) from p1  
)  
MyRound({CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)})  
```  
  
 A seguir está um exemplo de uma definição de tipo de LINHA.  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Row(x EDM.Decimal)) AS (  
   Round(p1.x)  
)  
select MyRound(row(a as x)) from {CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)} as a  
```  
  
 A seguir está um exemplo de uma definição de tipo de LINHA.  
  
```sql  
USING Microsoft.Samples.Entity  
Function UnReference(p1 Ref(AdventureWorks.Order)) AS (  
   Deref(p1)  
)  
select Ref(x) from AdventureWorksEntities.SalesOrderHeaders as x  
```  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
- [Referência de Entity SQL](entity-sql-reference.md)
