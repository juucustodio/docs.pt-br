---
description: 'Saiba mais sobre: funções de data e hora'
title: Funções de Data e Hora
ms.date: 03/30/2017
ms.assetid: 971762d0-663b-4b64-8c61-352a8e6d3949
ms.openlocfilehash: d8172a3b69f36c183d5288740d4a11e008a97428
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651022"
---
# <a name="date-and-time-functions"></a>Funções de Data e Hora

O provedor de dados. NET Framework para SQL Server (SqlClient) fornece funções de data e hora que executam operações em uma entrada de `System.DateTime` avalia e retorna um resultado de `string`, numérico, ou de `System.DateTime` de valor. Essas funções estão no namespace SqlServer, que está disponível quando você usa o SqlClient. A propriedade de namespace de um provedor permite que o Entity Framework descubra qual prefixo é usado por esse provedor para construções específicas, como tipos e funções. A tabela a seguir mostra as funções de data e hora SqlClient.  
  
|Função|Descrição|  
|--------------|-----------------|  
|`DATEADD(datepart, number, date)`|Retorna o novo valor `DateTime` com base na adição de um intervalo à data especificada.<br /><br /> **Argumentos**<br /><br /> `datepart`: `String` que representa a parte de data para retornar um novo valor.<br /><br /> `number`: `Int32`, `Int64`, `Decimal`, ou valor de `Double` usado para incrementar `datepart`.<br /><br /> `date:` Uma expressão que retorna um `DateTime` , ou `DateTimeOffset` ou `Time` com precisão = [0-7], ou uma cadeia de caracteres em um formato de data.<br /><br /> **Valor retornado**<br /><br /> Novo `DateTime`, ou `DateTimeOffset`, ou valor de `Time` com precisão = [] 0-7.<br /><br /> **Exemplo**<br /><br /> `SqlServer.DATEADD('day', 22, cast('6/9/2006' as DateTime))`|  
|`DATEDIFF(datepart,startdate,enddate)`|Retorna o número de limites de data e hora entre duas datas especificadas.<br /><br /> **Argumentos**<br /><br /> `datepart`: `String` que representa a parte de data para calcular a diferença.<br /><br /> `startdate`: Uma data de início para o cálculo é uma expressão que retorna `DateTime`, ou `DateTimeOffset`, ou valor de `Time` com precisão = [] 0-7, ou uma cadeia de caracteres em um formato de data.<br /><br /> `enddate:` Uma data de término para o cálculo é uma expressão que retorna um `DateTime` valor, ou `DateTimeOffset` ou `Time` com precisão = [0-7] ou uma cadeia de caracteres em um formato de data.<br /><br /> **Valor retornado**<br /><br /> Um `Int32`.<br /><br /> **Exemplo**<br /><br /> `SqlServer.DATEDIFF('day', cast('6/9/2006' as DateTime),`<br /><br /> `cast('6/20/2006' as DateTime))`|  
|`DATENAME(datepart, date)`|Retorna uma cadeia de caracteres que representa o datepart especificado de data especificada.<br /><br /> **Argumentos**<br /><br /> `datepart`: `String` que representa a parte de data para retornar um novo valor.<br /><br /> `date`: Uma expressão que retorna `DateTime,` ou `DateTimeOffset`, ou valor de `Time` com precisão = [] 0-7, ou uma cadeia de caracteres em um formato de data.<br /><br /> **Valor retornado**<br /><br /> A cadeia de caracteres que representa o datepart especificado de data especificada.<br /><br /> **Exemplo**<br /><br /> `SqlServer.DATENAME('year', cast('6/9/2006' as DateTime))`|  
|`DATEPART(datepart, date)`|Retorna um inteiro que representa o datepart especificado de data especificada.<br /><br /> **Argumentos**<br /><br /> `datepart`: `String` que representa a parte de data para retornar um novo valor.<br /><br /> `date`: Uma expressão que retorna `DateTime,` ou `DateTimeOffset,` ou valor de `Time` com precisão = [] 0-7, ou uma cadeia de caracteres em um formato de data.<br /><br /> **Valor retornado**<br /><br /> O datepart especificado de data especificada, como `Int32`.<br /><br /> **Exemplo**<br /><br /> `SqlServer.DATEPART('year', cast('6/9/2006' as DateTime))`|  
|`DAY(date)`|Retorna o dia da data especificada como um inteiro.<br /><br /> **Argumentos**<br /><br /> `date`: Uma expressão do tipo `DateTime` ou `DateTimeOffset` com precisão = 0-7.<br /><br /> **Valor retornado**<br /><br /> O dia de data especificada como `Int32`.<br /><br /> **Exemplo**<br /><br /> `SqlServer.DAY(cast('6/9/2006' as DateTime))`|  
|`GETDATE()`|Gerencia a data e hora no formato interno do SQL Server para valores de datetime.<br /><br /> **Valor retornado**<br /><br /> A data e hora atuais do sistema como `DateTime` com uma precisão de 3.<br /><br /> **Exemplo**<br /><br /> `SqlServer.GETDATE()`|  
|`GETUTCDATE()`|Gerencia o valor datetime no formato UTC (Tempo Universal Coordenado ou o horário de Greenwich) atuais.<br /><br /> **Valor retornado**<br /><br /> O valor de `DateTime` com uma precisão de 3 no formato UTC.<br /><br /> **Exemplo**<br /><br /> `SqlServer.GETUTCDATE()`|  
|`MONTH(date)`|Retorna o mês de data especificada como um número inteiro.<br /><br /> **Argumentos**<br /><br /> `date`: Uma expressão do tipo `DateTime` ou `DateTimeOffset` com precisão = 0-7.<br /><br /> **Valor retornado**<br /><br /> O mês de data especificada como `Int32`.<br /><br /> **Exemplo**<br /><br /> `SqlServer.MONTH(cast('6/9/2006' as DateTime))`|  
|`YEAR(date)`|Retorna o ano de data especificada como um número inteiro.<br /><br /> **Argumentos**<br /><br /> `date`: Uma expressão do tipo `DateTime` ou `DateTimeOffset` com precisão = 0-7.<br /><br /> **Valor retornado**<br /><br /> O ano de data especificada como `Int32`.<br /><br /> **Exemplo**<br /><br /> `SqlServer.YEAR(cast('6/9/2006' as DateTime))`|  
|`SYSDATETIME()`|Retorna um valor de `DateTime` com uma precisão de 7.<br /><br /> **Valor retornado**<br /><br /> Um valor de `DateTime` com uma precisão de 7.<br /><br /> **Exemplo**<br /><br /> `SqlServer.SYSDATETIME()`|  
|`SYSUTCDATE()`|Gerencia o valor datetime no formato UTC (Tempo Universal Coordenado ou o horário de Greenwich) atuais.<br /><br /> **Valor retornado**<br /><br /> O valor de `DateTime` com precisão = 7 no formato UTC.<br /><br /> **Exemplo**<br /><br /> `SqlServer.SYSUTCDATE()`|  
|`SYSDATETIMEOFFSET()`|Retorna `DateTimeOffset` com uma precisão de 7.<br /><br /> **Valor retornado**<br /><br /> Um valor de `DateTimeOffset` com precisão de 7 no formato UTC.<br /><br /> **Exemplo**<br /><br /> `SqlServer.SYSDATETIMEOFFSET()`|  
  
 Para obter mais informações sobre as funções de data e hora às quais o SqlClient dá suporte, consulte [tipos de dados e funções de data e hora (Transact-SQL)](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql).
  
## <a name="see-also"></a>Consulte também

- [SqlClient para funções de Entity Framework](sqlclient-for-ef-functions.md)
