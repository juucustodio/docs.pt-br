---
description: 'Saiba mais sobre: modelo conceitual canônico para SQL Server mapeamento de funções'
title: Modelo conceitual canônico a mapeamento de funções do SQL Server
ms.date: 03/30/2017
ms.assetid: 1a2631bc-a426-4c0a-ba8d-26d9c80d39e2
ms.openlocfilehash: 25e366a45e91db97693c42b3c8d2febd912320ab
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651061"
---
# <a name="conceptual-model-canonical-to-sql-server-functions-mapping"></a>Modelo conceitual canônico a mapeamento de funções do SQL Server

Este tópico descreve como o mapa canônico de funções modelo conceitual ao SQL Server correspondente funciona.  
  
## <a name="date-and-time-functions"></a>Funções de Data e Hora  

 A tabela a seguir descreve mapeamento de funções de data e hora:  
  
|Funções canônicas|Funções do SQL Server|  
|-------------------------|--------------------------|  
|[AddDays (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(day, number, date)`|  
|[AddHours (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(hour, number, date)`|  
|[AddMicroseconds (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(microsecond, number, date)`|  
|[AddMilliseconds (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(millisecond, number, date)`|  
|[AddMinutes (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(minute, number, date)`|  
|[AddMonths (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(month, number, date)`|  
|[AddNanoseconds (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(nanosecond, number, date)`|  
|[AddSeconds (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(second, number, date)`|  
|[AddYears (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DATEADD(year, number, date)`|  
|[CreateDateTime (ano, mês, dia, hora, minuto, conforme)](./language-reference/date-and-time-canonical-functions.md)|Para SQL Server 2000 e SQL Server 2005, um valor formatado `datetime` é criado no servidor. Para SQL Server 2008 e versões posteriores, um valor de `datetime2` é criado no servidor.|  
|[CreateDateTimeOffset (ano, mês, dia, hora, minuto, conforme, tzoffset)](./language-reference/date-and-time-canonical-functions.md)|Um valor formatado `datetimeoffset` é criado no servidor.<br /><br /> Não suportado no SQL Server 2000 ou no SQL Server 2005.|  
|[CreateTime (hora, minuto, segunda)](./language-reference/date-and-time-canonical-functions.md)|Um valor formatado `time` é criado no servidor.<br /><br /> Não suportado no SQL Server 2000 ou no SQL Server 2005.|  
|[CurrentDateTime()](./language-reference/date-and-time-canonical-functions.md)|`SysDateTime()` em SQLServer 2008.<br /><br /> `GetDate()` em SQLServer 2000 e em SQLServer 2005.|  
|[CurrentDateTimeOffset()](./language-reference/date-and-time-canonical-functions.md)|`SysDateTimeOffset()` no SQL Server 2008.<br /><br /> Não suportado no SQL Server 2000 ou no SQL Server 2005.|  
|[CurrentUtcDateTime()](./language-reference/date-and-time-canonical-functions.md)|`SysUtcDateTime()` em SQLServer 2008. `GetUtcDate()` no SQL Server 2000 e no SQL Server 2005.|  
|[DayOfYear (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(dayofyear, expression)`|  
|[Dia (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(day, expression)`|  
|[DiffDays (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(day, startdate, enddate)`|  
|[DiffHours (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(hour, startdate, enddate)`|  
|[DiffMicroseconds (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(microsecond, startdate, enddate)`|  
|[DiffMilliseconds (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(millisecond, startdate, enddate)`|  
|[DiffMinutes (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(minute, startdate, enddate)`|  
|[DiffNanoseconds (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(nanosecond, startdate, enddate)`|  
|[DiffSeconds (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(second, startdate, enddate)`|  
|[DiffYears (startExpression, endExpression)](./language-reference/date-and-time-canonical-functions.md)|`DATEDIFF(year, startdate, enddate)`|  
|[GetTotalOffsetMinutes (DateTimeOffset)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(tzoffset, expression)`|  
|[Hora (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(hour, expression)`|  
|[Milissegundos (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(millisecond, expression)`|  
|[Minuto (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(minute, expression)`|  
|[Mês (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(month, expression)`|  
|[Segundo (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(second, expression)`|  
|[Truncar (expressão)](./language-reference/date-and-time-canonical-functions.md)|Para SQL Server 2000 e SQL Server 2005, um `datetime` valor formatado truncado é criado no servidor. Para SQL Server 2008 e versões posteriores, um truncado `datetime2` ou `datetimeoffset` valor é criado no servidor.|  
|[Ano (expressão)](./language-reference/date-and-time-canonical-functions.md)|`DatePart(YEAR, expression)`|  
  
## <a name="aggregate-functions"></a>Funções de Agregação  

 A tabela a seguir descreve mapeamento de funções agregadas:  
  
|Funções canônicas|Funções do SQL Server|  
|-------------------------|--------------------------|  
|[Avg (expressão)](./language-reference/aggregate-canonical-functions.md)|`AVG(expression)`|  
|[BigCount (expressão)](./language-reference/aggregate-canonical-functions.md)|`BIGCOUNT(expression)`|  
|[Contagem (expressão)](./language-reference/aggregate-canonical-functions.md)|`COUNT(expression)`|  
|[Minuto (expressão)](./language-reference/aggregate-canonical-functions.md)|`MIN(expression)`|  
|[Máximo (expressão)](./language-reference/aggregate-canonical-functions.md)|`MAX(expression)`|  
|[StDev (expressão)](./language-reference/aggregate-canonical-functions.md)|`STDEV(expression)`|  
|[StDevP (expressão)](./language-reference/aggregate-canonical-functions.md)|`STDEVP(expression)`|  
|[Soma (expressão)](./language-reference/aggregate-canonical-functions.md)|`SUM(expression)`|  
|[Var (expressão)](./language-reference/aggregate-canonical-functions.md)|`VAR(expression)`|  
|[VarP (expressão)](./language-reference/aggregate-canonical-functions.md)|`VARP(expression)`|  
  
## <a name="math-functions"></a>Funções matemáticas  

 A tabela a seguir descreve mapeamento de funções matemáticas:  
  
|Funções canônicas|Funções do SQL Server|  
|-------------------------|--------------------------|  
|[Abs (valor)](./language-reference/math-canonical-functions.md)|`ABS(value)`|  
|[Teto (valor)](./language-reference/math-canonical-functions.md)|`CEILING(value)`|  
|[Andar (valor)](./language-reference/math-canonical-functions.md)|`FLOOR(value)`|  
|[Avançados (valor)](./language-reference/math-canonical-functions.md)|`POWER(value, exponent)`|  
|[Redondo (valor)](./language-reference/math-canonical-functions.md)|`ROUND(value, digits, 0)`|  
|[Truncate](./language-reference/math-canonical-functions.md)|`ROUND(value , digits, 1)`|  
  
## <a name="string-functions"></a>Funções de Cadeia de Caracteres  

 A tabela a seguir descreve mapeamento de funções de cadeia de caracteres:  
  
|Funções canônicas|Funções do SQL Server|  
|-------------------------|--------------------------|  
|[Contém (cadeia de caracteres, destino)](./language-reference/string-canonical-functions.md)|`CHARINDEX(target, string)`|  
|[Concat (string1, string2)](./language-reference/string-canonical-functions.md)|string1 + string2|  
|[EndsWith (cadeia de caracteres, destino)](./language-reference/string-canonical-functions.md)|`CHARINDEX(REVERSE(target), REVERSE(string)) = 1`<br /><br /> **Observação** A `CHARINDEX` função retornará `false` se o `string` for armazenado em uma coluna de cadeia de caracteres de comprimento fixo e `target` for uma constante. Nesse caso, a cadeia de caracteres inteira é pesquisada, incluindo todos os espaço à direita de preenchimento. Uma solução alternativa é possível quebrar dados a cadeia de caracteres fixa de comprimento antes de passar a cadeia de caracteres a função de `EndsWith` , como no exemplo a seguir: `EndsWith(TRIM(string), target)`|  
|[IndexOf (destino), string2](./language-reference/string-canonical-functions.md)|`CHARINDEX(target, string2)`|  
|[Esquerda (string1, comprimento)](./language-reference/string-canonical-functions.md)|`LEFT(string1, length)`|  
|[Comprimento (cadeia de caracteres)](./language-reference/string-canonical-functions.md)|`LEN(string)`|  
|[LTrim (cadeia de caracteres)](./language-reference/string-canonical-functions.md)|`LTRIM(string)`|  
|[Direito (string1, comprimento)](./language-reference/string-canonical-functions.md)|`RIGHT (string1, length)`|  
|[Preparo (cadeia de caracteres)](./language-reference/string-canonical-functions.md)|`LTRIM(RTRIM(string))`|  
|[Substitua (string1, string2, string3)](./language-reference/string-canonical-functions.md)|`REPLACE(string1, string2, string3)`|  
|[Inversa (cadeia de caracteres)](./language-reference/string-canonical-functions.md)|`REVERSE (string)`|  
|[RTrim (cadeia de caracteres)](./language-reference/string-canonical-functions.md)|`RTRIM(string)`|  
|[StartsWith (cadeia de caracteres, destino)](./language-reference/string-canonical-functions.md)|`CHARINDEX(target, string)`|  
|[Subsequência de caracteres (cadeia de caracteres, iniciar, comprimento)](./language-reference/string-canonical-functions.md)|`SUBSTRING(string, start, length)`|  
|[ToLower (cadeia de caracteres)](./language-reference/string-canonical-functions.md)|`LOWER(string)`|  
|[ToUpper (cadeia de caracteres)](./language-reference/string-canonical-functions.md)|`UPPER(string)`|  
  
## <a name="bitwise-functions"></a>Funções bit a bit  

 A tabela a seguir descreve mapear bit a bit das funções:  
  
|Funções canônicas|Funções do SQL Server|  
|-------------------------|--------------------------|  
|[BitWiseAnd (valor1, valor2)](./language-reference/bitwise-canonical-functions.md)|value1 & value2|  
|[BitWiseNot (valor)](./language-reference/bitwise-canonical-functions.md)|~value|  
|[BitWiseOr (valor1, valor2)](./language-reference/bitwise-canonical-functions.md)|value1 &#124; value2|  
|[BitWiseXor (valor1, valor2)](./language-reference/bitwise-canonical-functions.md)|valor2 de ^ de valor1|
