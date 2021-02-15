---
description: 'Saiba mais sobre: funções canônicas de matemática'
title: Funções canônicas matemáticas
ms.date: 03/30/2017
ms.assetid: 6f6cddc6-b561-4ebe-84b6-841ef5b4113b
ms.openlocfilehash: 55072099f5766d48ea3067a2e9eaa187a8b3f111
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739359"
---
# <a name="math-canonical-functions"></a>Funções canônicas matemáticas

Entity SQL inclui as seguintes funções canônicas de matemática:
  
## <a name="absvalue"></a>Abs (valor)

Retorna o valor absoluto de `value`.

**Argumentos**

Um `Int16` , `Int32` , `Int64` , `Byte` , `Single` , `Double` e `Decimal` .

**Valor retornado**

O tipo de `value`.

**Exemplo**

`Abs(-2)`

## <a name="ceilingvalue"></a>Teto (valor)

Retorna o número inteiro o menor que não é menor que `value`.

**Argumentos**

A `Single` , `Double` , e `Decimal` .

**Valor retornado**

O tipo de `value`.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_CEILING](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_ceiling)]
[!code-sql[DP EntityServices Concepts#EDM_CEILING](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_ceiling)]

## <a name="floorvalue"></a>Andar (valor)

Retorna o número inteiro maior que não é maior do que `value`.

**Argumentos**

A `Single` , `Double` , e `Decimal` .

**Valor retornado**

O tipo de `value`.

**Exemplo**

[!code-csharp[DP EntityServices Concepts#EDM_FLOOR](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_floor)]
[!code-sql[DP EntityServices Concepts#EDM_FLOOR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_floor)]

## <a name="powervalue-exponent"></a>Põe (valor, expoente)

Retorna o resultado de `value` especificado a `exponent`especificado.

**Argumentos**

|  |  |
|--|--|
|`value` | Um `Int32, Int64, Double` ou `Decimal`. |
|`exponent` | Um `Int64` , `Double` , ou `Decimal` . |

**Valor retornado**

O tipo de `value`.

**Exemplo**

`Power(748.58,2)`

## <a name="roundvalue"></a>Redondo (valor)

Retorna a parte inteira de `value`, arredondada para o inteiro mais próximo.

**Argumentos**

A `Single` , `Double` , e `Decimal` .

**Valor retornado**

O tipo de `value`.

**Exemplo**

`Round(748.58)`

## <a name="roundvalue-digits"></a>Redondo (valor, dígitos)

Retorna `value`, arredondado a `digits`especificado o mais próximo.

**Argumentos**

|  |  |
|--|--|
|`value`|`Double` ou `Decimal`.|
|`digits`|`Int16` ou `Int32`.|

**Valor retornado**

O tipo de `value`.

**Exemplo**

`Round(748.58,1)`

## <a name="truncatevalue-digits"></a>Truncar (valor, dígitos)

Retorna `value`, truncado a `digits`especificado o mais próximo.

**Argumentos**

|  |  |
|--|--|
|`value`|`Double` ou `Decimal`.|
|`digits`|`Int16` ou `Int32`.|

**Valor retornado**

O tipo de `value`.

**Exemplo**

`Truncate(748.58,1)`  
  
 Essas funções retornará `null` se entrada dada de `null` .  
  
 Funcionalidade equivalente está disponível no provedor gerenciado cliente do Microsoft SQL. Para obter mais informações, consulte [SqlClient para funções de Entity Framework](../sqlclient-for-ef-functions.md).  
  
## <a name="see-also"></a>Consulte também

- [Funções canônicas](canonical-functions.md)
