---
description: 'Saiba mais sobre: funções canônicas de data e hora'
title: Funções canônicas de data e hora
ms.date: 03/30/2017
ms.assetid: 9628b74f-1585-436a-b385-8b02ed0cdd63
ms.openlocfilehash: 3c57edc613e5ef871aa3359ef7609e6c0892efc4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724785"
---
# <a name="date-and-time-canonical-functions"></a>Funções canônicas de data e hora

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] inclui funções canônicas de data e hora.  
  
## <a name="remarks"></a>Comentários  

 A tabela a seguir mostra as funções canônicas de data e hora [!INCLUDE[esql](../../../../../../includes/esql-md.md)] . `datetime` é um <xref:System.DateTime> valor.  
  
|Função|Descrição|  
|--------------|-----------------|  
|`AddNanoseconds(expression,number)`|Adiciona `number` especificado de nanossegundos a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime`, `DateTimeOffset`, ou `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddMicroseconds(expression,number)`|Adiciona `number` especificado de microssegundos a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime`, `DateTimeOffset`, ou `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddMilliseconds(expression,number)`|Adiciona `number` especificado de milissegundos a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime`, `DateTimeOffset`, ou `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddSeconds(expression,number)`|Adiciona `number` especificado de segundos a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime`, `DateTimeOffset`, ou `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddMinutes(expression,number)`|Adiciona `number` especificado de minutos a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime`, `DateTimeOffset`, ou `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddHours(expression,number)`|Adiciona `number` especificado hora a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime`, `DateTimeOffset`, ou `Time`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddDays(expression,number)`|Adiciona `number` especificado de dias a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime` ou `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddMonths(expression,number)`|Adiciona `number` especificado de meses a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime` ou `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`AddYears(expression,number)`|Adiciona `number` especificado de anos a `expression`.<br /><br /> **Argumentos**<br /><br /> `expression`: `DateTime` ou `DateTimeOffset`.<br /><br /> `number`: `Int32`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`CreateDateTime(year,month,day,hour,minute,second)`|Retorna um novo valor de `DateTime` como a data e hora atuais do servidor na zona de tempo do servidor.<br /><br /> **Argumentos**<br /><br /> `year`, `month`, `day`, `hour`, `minute`: `Int16` e `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Valor retornado**<br /><br /> Um `DateTime`.|  
|`CreateDateTimeOffset(year,month,day,hour,minute,second,tzoffset)`|Retorna um novo valor de `DateTimeOffset` como a data e hora atuais do servidor relativo ao Tempo Universal Coordenado (UTC).<br /><br /> **Argumentos**<br /><br /> `year`, `month`, `day`, `hour`, `minute`, `tzoffset`: `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Valor retornado**<br /><br /> Um `DateTimeOffset`.|  
|`CreateTime(hour,minute,second)`|Retorna um novo valor de `Time` como a hora atual.<br /><br /> **Argumentos**<br /><br /> `hour` e `minute`: `Int32`.<br /><br /> `second`: `Double`.<br /><br /> **Valor retornado**<br /><br /> Um `Time`.|  
|`CurrentDateTime()`|Retorna um valor de `DateTime` como a data e hora atuais do servidor na zona de tempo do servidor.<br /><br /> **Valor retornado**<br /><br /> Um `DateTime`.|  
|`CurrentDateTimeOffset()`|Retorna a data atual, hora e o deslocamento como `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `DateTimeOffset`.|  
|`CurrentUtcDateTime()`|Retorna um valor de <xref:System.DateTime> como a data e hora atuais do servidor na zona de UTS.<br /><br /> **Valor retornado**<br /><br /> Um `DateTime`.|  
|`Day(expression)`|Retorna a parte do dia de `expression` como `Int32` entre 1 e 31.<br /><br /> **Argumentos**<br /><br /> `DateTime` e `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 12.`<br /><br /> `Day(cast('03/12/1998' as DateTime))`|  
|`DayOfYear(expression)`|Retorna a parte do dia de `expression` como `Int32` entre 1 e 366, onde 366 são retornados para o último dia de um ano bissexto.<br /><br /> **Argumentos**<br /><br /> `DateTime` ou `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffNanoseconds(startExpression,endExpression)`|Retorna a diferença, em nanossegundos, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset`, ou `Time`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffMilliseconds(startExpression,endExpression)`|Retorna a diferença, em milissegundos, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset`, ou `Time`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffMicroseconds(startExpression,endExpression)`|Retorna a diferença, em microssegundos, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset`, ou `Time`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffSeconds(startExpression,endExpression)`|Retorna a diferença, em segundos, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset`, ou `Time`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffMinutes(startExpression,endExpression)`|Retorna a diferença, em minutos, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset`, ou `Time`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffHours(startExpression,endExpression)`|Retorna a diferença, hora, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime`, `DateTimeOffset`, ou `Time`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffDays(startExpression,endExpression)`|Retorna a diferença, os dias, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime` ou `DateTimeOffset`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffMonths(startExpression,endExpression)`|Retorna a diferença, em meses, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime` ou `DateTimeOffset`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`DiffYears(startExpression,endExpression)`|Retorna a diferença, em anos, entre `startExpression` e `endExpression`.<br /><br /> **Argumentos**<br /><br /> `startExpression`, `endExpression`: `DateTime` ou `DateTimeOffset`. **Observação:** `startExpression` e `endExpression` devem ser do mesmo tipo.   <br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`GetTotalOffsetMinutes(datetimeoffset)`|Retorna o número de minutos que `datetimeoffset` é deslocado GMT. Isso é geralmente entre +780 e -780 (+ ou - 13 horas). **Observação:**  Essa função tem suporte somente no SQL Server 2008. <br /><br /> **Argumentos**<br /><br /> Um `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`Hour(expression)`|Retorna a parte da hora de `expression` como `Int32` entre 0 e 23.<br /><br /> **Argumentos**<br /><br /> `DateTime, Time` e `DateTimeOffset`.<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 22.`<br /><br /> `Hour(cast('22:35:5' as DateTime))`|  
|`Millisecond(expression)`|Retorna a parte de milissegundos de `expression` como `Int32` entre 0 e 999.<br /><br /> **Argumentos**<br /><br /> `DateTime, Time` e `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.|  
|`Minute(expression)`|Retorna a parte minúscula de `expression` como `Int32` entre 0 e 59.<br /><br /> **Argumentos**<br /><br /> `DateTime, Time` ou `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 35`<br /><br /> `Minute(cast('22:35:5' as DateTime))`|  
|`Month(expression)`|Retorna a parte do mês de `expression` como `Int32` entre 1 e 12.<br /><br /> **Argumentos**<br /><br /> `DateTime` ou `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 3.`<br /><br /> `Month(cast('03/12/1998' as DateTime))`|  
|`Second(expression)`|Retorna a parte de segundos de `expression` como `Int32` entre 0 e 59.<br /><br /> **Argumentos**<br /><br /> `DateTime, Time` e `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 5`<br /><br /> `Second(cast('22:35:5' as DateTime))`|  
|`TruncateTime(expression)`|Retorna `expression`, com os valores de tempo truncados.<br /><br /> **Argumentos**<br /><br /> `DateTime` ou `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> O tipo de `expression`.|  
|`Year(expression)`|Retorna a parte do ano de `expression` como um `Int32` `YYYY` .<br /><br /> **Argumentos**<br /><br /> `DateTime` e `DateTimeOffset`.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.<br /><br /> **Exemplo**<br /><br /> `-- The following example returns 1998.`<br /><br /> `Year(cast('03/12/1998' as DateTime))`|  
  
 Essas funções retornará `null` se entrada dada de `null` .  
  
 Funcionalidade equivalente está disponível no provedor gerenciado cliente do Microsoft SQL. Para obter mais informações, consulte [SqlClient para funções de Entity Framework](../sqlclient-for-ef-functions.md).  
  
## <a name="see-also"></a>Consulte também

- [Funções canônicas](canonical-functions.md)
