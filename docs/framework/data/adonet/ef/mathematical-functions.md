---
description: 'Saiba mais sobre: funções matemáticas'
title: Funções Matemáticas
ms.date: 03/30/2017
ms.assetid: b040c7cb-156d-40f2-9152-61065b18148c
ms.openlocfilehash: 6bf1f116d6d88a8a188dc31cab91fbf26bdaea36
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795021"
---
# <a name="mathematical-functions"></a>Funções Matemáticas

O provedor de dados. NET Framework para SQL Server (SqlClient) fornece as funções matemáticas que executam cálculos nos valores de entrada que são fornecidos como argumentos, e retorna um resultado de valor numérico. Essas funções estão no namespace SqlServer, que está disponível quando você usa o SqlClient. A propriedade de namespace de um provedor permite que o Entity Framework descubra qual prefixo é usado por esse provedor para construções específicas, como tipos e funções. A tabela a seguir descreve as funções matemáticas do SqlClient.  
  
## <a name="absexpression"></a>ABS (expressão)

Executa a função de valor absoluto.

**Argumentos**

`expression`: Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Valor retornado**

O valor absoluto de expressão especificada.

**Exemplo**

`SqlServer.ABS(-2)`

## <a name="acosexpression"></a>ACOS (expressão)

Retorna o valor de arccosine de expressão especificada.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.ACOS(.9)`

## <a name="asinexpression"></a>Asen (expressão)

Retorna o valor de arcsine de expressão especificada.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.ASIN(.9)`

## <a name="atanexpression"></a>ATAN (expressão)

Retorna o valor de arctangent de expressão numérica especificada.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.ATAN(9)`

## <a name="atn2expression-expression"></a>ATN2 (expressão, expressão)

Retorna o ângulo, em radianos, cuja tangente é entre as duas expressões numéricas especificadas.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.ATN2(9, 8)`

## <a name="ceilingexpression"></a>TETO (expressão)

Converte a expressão especificada para o inteiro menor que é maior ou igual a ele.

**Argumentos**

`expression`: Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Valor retornado**

Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Exemplo**

[!code-sql[DP EntityServices Concepts#SQLSERVER_CEILING](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_ceiling)]

## <a name="cosexpression"></a>COS (expressão)

Calcula o cosseno trigonométricas do ângulo especificado em radianos.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.COS(45)`

## <a name="cotexpression"></a>COT (expressão)

Calcula o cotangente trigonométricas do ângulo especificado em radianos.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.COT(60)`
  
## <a name="degreesradians"></a>GRAUS (radianos)

Retorna o ângulo correspondente em graus.

**Argumentos**

`expression`: Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Valor retornado**

Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Exemplo**

`SqlServer.DEGREES(3.1)`

## <a name="expexpression"></a>EXP (expressão)

Calcula o valor exponencialmente de uma expressão numérica especificada.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**`SqlServer.EXP(1)`

## <a name="floorexpression"></a>FLOOR (expressão)

Converte a expressão especificada para o inteiro maior menor ou igual a ele.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

[!code-sql[DP EntityServices Concepts#SQLSERVER_FLOOR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_floor)]

## <a name="logexpression"></a>LOG (expressão)

Calcula o logaritmo natural da expressão especificada de `float` .

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.LOG(100)`

## <a name="log10expression"></a>LOG10 (expressão)

Retorna o logaritmo base-10 de expressão especificada de `Double` .

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.LOG10(100)`

## <a name="pi"></a>PI ()

Retorna o valor constante de pi como `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.PI()`

## <a name="powernumeric_expression-power_expression"></a>ENERGIA (numeric_expression, power_expression)

Calcula o valor de uma expressão especificada em uma potência especificada.

**Argumentos**

|  |  |
|--|--|
|`numeric_expression`| Um `Int32` , `Int64` , `Double` ou `Decimal` .|
|`power_expression`| Um `Double` que representa o poder para o qual gerar o `numeric_expression` .|

**Valor retornado**

O valor de `numeric_expression` especificado a `power_expression`especificado.

**Exemplo**

`SqlServer.POWER(2,7)`

## <a name="radiansexpression"></a>RADIANOs (expressão)

Converte graus em radianos.

**Argumentos**

`expression`: Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Valor retornado**

Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Exemplo**

`SqlServer.RADIANS(360.0)`

## <a name="randseed"></a>RAND ([semente])

Retorna um valor aleatório de 0 a 1.

**Argumentos**

O valor de semente como um `Int32` . Se a semente não for especificada, o mecanismo de base de dados SQL Server atribui um valor semente aleatoriamente. Para um valor de semente especificado, o resultado retornado é sempre o mesmo.

**Valor retornado**

Um valor aleatório de 0 a 1. de `Double` .

**Exemplo**

`SqlServer.RAND()`
  
## <a name="roundnumeric_expression-lengthfunction"></a>ROUND (numeric_expression, comprimento [, função])

Retorna uma expressão numérica, arredondada para o comprimento ou a precisão especificada.

**Argumentos**

|  |  |
|--|--|
|`numeric_expression`| Um `Int32` , `Int64` , `Double` ou `Decimal` .
|`length`| Um `Int32` que representa a precisão a `numeric_expression` ser arredondado. Quando `length` é um número positivo, `numeric_expression` ele é arredondado para o número de posições decimais especificadas por `length`. Quando `length` é um número negativo, `numeric_expression` é arredondado no lado esquerdo do ponto decimal, como especificado por `length`.|
|`function` | Opcional. Um `Int32` que representa o tipo de operação a ser executada. Quando a função é omitida ou tem um valor de 0 (padrão), `numeric_expression` é arredondado. Quando um valor diferente de 0 é especificado, `numeric_expression` é truncado. |

**Valor retornado**

O valor de `numeric_expression` especificado a `power_expression`especificado.

**Exemplo**

`SqlServer.ROUND(748.58, -3)`

## <a name="signexpression"></a>ASSINAR (expressão)

Retorna o sinal positivo (+1), zero (0) ou sinal negativo (-1) da expressão especificada.

**Argumentos**

`expression`: `Int32`, `Int64`, `Double` ou `Decimal`

**Valor retornado**

Um `Int32` , `Int64` , `Double` ou `Decimal` .

**Exemplo**

`SqlServer.SIGN(-10)`

## <a name="sinexpression"></a>SIN (expressão)

Calcula o seno trigonométricas do ângulo especificado em radianos, e retorna uma expressão de `Double` .

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**`SqlServer.SIN(20)`

## <a name="sqrtexpression"></a>SQRT (expressão)

Retorna a raiz quadrada de expressão especificada.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**`SqlServer.SQRT(3600)`

## <a name="squareexpression"></a>SQUARE (expressão)

Retorna o quadrado de expressão especificada.

**Argumentos**

`expression`: um `Double`.

**Valor retornado**

Um `Double`.

**Exemplo**

`SqlServer.SQUARE(25)`

## <a name="tanexpression"></a>TAN (expressão)

Calcula a tangente de uma expressão especificada.

**Argumentos**

`expression`: `Double`

**Valor retornado**

`Double`

**Exemplo**

`SqlServer.TAN(45.0)`
  
## <a name="see-also"></a>Consulte também

- [Funções matemáticas (Transact-SQL)](/sql/t-sql/functions/mathematical-functions-transact-sql)
- [SqlClient para funções de Entity Framework](sqlclient-for-ef-functions.md)
