---
description: 'Saiba mais sobre: literais nulos e inferência de tipos (Entity SQL)'
title: Literais nulos e inferência de tipo (Entity SQL)
ms.date: 03/30/2017
ms.assetid: edd56afb-af1b-4e7d-b210-cb8998143426
ms.openlocfilehash: 3b3474ea9841a34970d2269173d263fda2eb1789
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802132"
---
# <a name="null-literals-and-type-inference-entity-sql"></a>Literais nulos e inferência de tipo (Entity SQL)

Literais nulos são compatíveis com qualquer no sistema de tipos de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] . No entanto, para que o tipo de um literal nulo seja inferido corretamente, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] o impõe certas restrições em que um literal nulo pode ser usado.  
  
## <a name="typed-nulls"></a>Tipado nulos  

 Tipado anula pode ser usado em qualquer lugar. Inferência de tipos não é necessária para tipado anula porque o tipo é conhecido. Por exemplo, você pode construir um zero do tipo Int16 com a seguir compilação de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] :  
  
 `(cast(null as Int16))`  
  
## <a name="free-floating-null-literals"></a>Literais nulos de flutuante  

 Literais nulos de flutuante podem ser usados nos seguintes contextos:  
  
- Como um argumento para uma expressão de CAST ou de DELEITE. Essa é a maneira recomendada para gerar uma expressão nula tipada.  
  
- Como um argumento para um método ou a uma função. As regras padrões de sobrecarga se aplicam.  
  
- Como um dos argumentos para uma expressão aritmética como +, -, ou a/. Os outros argumentos não podem ser nulos literais, se não inferência de tipos não é possível.  
  
- Como alguns dos argumentos para uma expressão (lógica AND, OU, ou NÃO). Todos os argumentos são conhecidos para ser do tipo booleano.  
  
- Como o argumento para o É NULL ou NÃO É expressão NULA.  
  
- Como um ou mais dos argumentos a GOSTE da expressão. Todos os argumentos sejam cadeias de caracteres.  
  
- Como um ou mais dos argumentos para um construtor de nomeadas tipo.  
  
- Como um ou mais dos argumentos para um construtor de multiset. Pelo menos um argumento para o construtor de multiset deve ser uma expressão que não seja um literal nulo.  
  
- Como uma ou mais de ENTÃO DE ou em expressões em uma expressão de CASOS. Pelo menos uma de ENTÃO DE ou em expressões na expressão de CASOS deve ser uma expressão que não seja um literal nulo.  
  
 Literais nulos de flutuante não podem ser usados em outros cenários. Por exemplo, não podem ser usados como argumentos para um construtor de linha.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
