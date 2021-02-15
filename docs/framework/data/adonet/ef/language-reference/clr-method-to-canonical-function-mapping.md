---
description: 'Saiba mais sobre: método CLR para mapeamento de função canônica'
title: Método CLR ao mapeamento canônico de função
ms.date: 03/30/2017
ms.assetid: e3363261-2cb8-4b54-9555-2870be99b929
ms.openlocfilehash: 3a082f0b9bce63330e113e6ae9f50d15d71ce727
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99697069"
---
# <a name="clr-method-to-canonical-function-mapping"></a>Método CLR ao mapeamento canônico de função

Entity Framework fornece um conjunto de funções canônicas que implementam a funcionalidade que são comuns através de muitos sistemas de base de dados, como a manipulação de cadeia de caracteres e funções matemáticas. Isso permite aos desenvolvedores para direcionar uma ampla gama de sistemas de base de dados. Quando chamadas de uma tecnologia consultando, como LINQ to Entities, essas funções canônicas são transmitidos para a função correspondente correta do armazenamento para o provedor que está sendo usado. Isso permite que as chamadas de função são expressos em um formulário comuns através de fontes de dados, fornecendo uma experiência consistente de consulta por de fontes de dados. Os operadores bit e, OR, NOT e XOR também são mapeados para funções canônicas quando o operando é um tipo numérico. Para os operandos boolianos, os operadores AND, and, NOT e XOR de and lógico computem as operações lógica AND, OR, and e XOR de seus operandos. Para obter mais informações, consulte [funções canônicas](canonical-functions.md).

Para cenários LINQ, as consultas em Entity Framework envolvem mapear determinados métodos de CLR métodos na fonte de dados subjacente com as funções canônicas. Todas as chamadas de método em consulte LINQ to entidades que não são mapeados explicitamente a uma função canônica resultarão em uma exceção de <xref:System.NotSupportedException> de runtime que está sendo lançada.

## <a name="systemstring-method-static-mapping"></a>Mapear de método System.String (estático)

|Método System.String (estático)|Função canônica|
|-------------------------------------|------------------------|
|Concat System.String (cadeia de caracteres `str0`, cadeia de caracteres `str1`)|Concat (`str0`, `str1`)|
|Concat System.String (cadeia de caracteres `str0`, cadeia de caracteres `str1`, cadeia de caracteres `str2`)|Concat (Concat (`str0`, `str1`), `str2`)|
|Concat System.String (cadeia de caracteres `str0`, cadeia de caracteres `str1`, cadeia de caracteres `str2`, cadeia de caracteres `str03`)|Concat (Concat (Concat (`str0`, `str1`), `str2`), `str3`)|
|Iguais booleanas (cadeia de caracteres `a`, cadeia de caracteres `b`)|Operador =|
|IsNullOrEmpty booleano (cadeia de caracteres `value`)|(IsNull (`value`)) OU comprimento (`value`= 0)|
|Op_Equality booleano (cadeia de caracteres `a`, cadeia de caracteres `b`)|Operador =|
|Op_Inequality booleano (cadeia de caracteres `a` , cadeia de caracteres `b`)|Operador !=|
|Microsoft.VisualBasic.Strings.Trim (cadeia de caracteres `str`)|Preparo (`str`)|
|Microsoft.VisualBasic.Strings.LTrim (cadeia de caracteres `str`)|Ltrim (`str`)|
|Microsoft.VisualBasic.Strings.RTrim (cadeia de caracteres `str`)|Rtrim (`str`)|
|Microsoft.VisualBasic.Strings.Len (cadeia de caracteres `expression`)|Comprimento (`expression`)|
|Microsoft.VisualBasic.Strings.Left (cadeia de caracteres `str`, Int32 `Length`)|Esquerda (`str`, `Length`)|
|Microsoft.VisualBasic.Strings.Mid (cadeia de caracteres `str`, Int32 `Start`, Int32 `Length`)|Subsequência de caracteres (`str`, `Start`, `Length`)|
|Microsoft.VisualBasic.Strings.Right (cadeia de caracteres `str`, Int32 `Length`)|Direito (`str`, `Length`)|
|Microsoft.VisualBasic.Strings.UCase (cadeia de caracteres `Value`)|ToUpper (`Value`)|
|Microsoft.VisualBasic.Strings.LCase (valor de cadeia de caracteres)|ToLower (`Value`)|

## <a name="systemstring-method-instance-mapping"></a>Mapear de método System.String (instância)

|Método de instância System.String ()|Função canônica|Observações|
|---------------------------------------|------------------------|-----------|
|Boolean contém (cadeia de caracteres `value`)|`this` GOSTA de “% de`value`%”|Se `value` não for uma constante, isso será mapeado para IndexOf ( `this` , `value` ) > 0|
|EndsWith booleano (cadeia de caracteres `value`)|`this`LIKE `'` % `value` '|Se `value` não é uma constante, então este mapeados para a direita (`this`,`value`comprimento ()) = `value`.|
|StartsWith booleano (cadeia de caracteres `value`)|`this` GOSTA de '`value`% "|Se `value` não é uma constante, então este mapeia para IndexOf (`this`, `value`) = 1.|
|Comprimento|Comprimento (`this`)||
|Int32 IndexOf (cadeia de caracteres `value`)|IndexOf (`this`, `value`) - 1||
|Inserção de System.String (Int32, `startIndex`cadeia de caracteres `value`)|Concat (Concat (subcadeia de caracteres (`this`, 1, `startIndex`), `value`), subcadeia de caracteres (`this`, `startIndex`+1, comprimento (`this`) - `startIndex`))||
|System.String remove (Int32 `startIndex`)|Subsequência de caracteres (`this`, 1, `startIndex`)||
|System.String remove (Int32 `startIndex`, Int32 `count`)|Concat (Subcadeia de caracteres ( `this` , 1, `startIndex` ), subcadeia de caracteres ( `this` , `startIndex`  +  `count` + 1, comprimento ( `this` )-( `startIndex`  +  `count` ))|Remova (`startIndex`, `count`) é suportado apenas se `count` é um inteiro maior ou igual a 0.|
|System.String substituem (cadeia de caracteres `oldValue`, cadeia de caracteres `newValue`)|Substitua (`this`, `oldValue`, `newValue`)||
|Subsequência de caracteres de System.String (Int32 `startIndex`)|Subsequência de caracteres (`this`, `startIndex` +1, comprimento (`this`) - `startIndex`)||
|Subsequência de caracteres de System.String (Int32 `startIndex`, Int32 `length`)|Subcadeia de caracteres ( `this` , `startIndex` + 1, `length` )||
|System.String ToLower()|ToLower (`this`)||
|System.String ToUpper()|ToUpper (`this`)||
|System.String Trim()|Preparo (`this`)||
|System.String TrimEnd char ([]) `trimChars`|RTrim (`this`)||
|System.String TrimStart char ([])`trimChars`|LTrim (`this`)||
|Iguais booleanas (cadeia de caracteres `value`)|Operador =||

## <a name="systemdatetime-method-static-mapping"></a>Mapear de método System.DateTime (estático)

|Método System.DateTime (estático)|Função canônica|Observações|
|---------------------------------------|------------------------|-----------|
|Iguais booleanas (DateTime `t1`, DateTime `t2`)|Operador =||
|System.DateTime.Now|CurrentDateTime()||
|System.DateTime.UtcNow|CurrentUtcDateTime()||
|Op_Equality booleano (DateTime `d1`, DateTime `d2`)|Operador =||
|Op_GreaterThan booleano (DateTime `t1`, DateTime `t2`)|Operador de >||
|Op_GreaterThanOrEqual booleano (DateTime `t1`, DateTime `t2`)|Operador >=||
|Op_Inequality booleano (DateTime `t1`, DateTime `t2`)|Operador !=||
|Op_LessThan booliano (DateTime `t1` , DateTime `t2` )|Operador de <||
|Op_LessThanOrEqual booleano (DateTime `t1`, DateTime `t2`)|Operador <=||
|Microsoft.VisualBasic.DateAndTime.DatePart (_<br /><br /> ByVal `Interval` as DateInterval, \_<br /><br /> ByVal `DateValue` as DateTime, \_<br /><br /> Opcional ByVal `FirstDayOfWeekValue` as FirstDayOfWeek = VbSunday, \_<br /><br /> ByVal opcional `FirstWeekOfYearValue` como FirstWeekOfYear = VbFirstJan1 \_<br /><br /> Como o inteiro)||Consulte a seção de função DatePart para mais informações.|
|Microsoft.VisualBasic.DateAndTime.Now|CurrentDateTime()||
|Microsoft.VisualBasic.DateAndTime.Year (DateTime `TimeValue`)|Year()||
|Microsoft.VisualBasic.DateAndTime.Month (DateTime `TimeValue`)|Month()||
|Microsoft.VisualBasic.DateAndTime.Day (DateTime `TimeValue`)|Day()||
|Microsoft.VisualBasic.DateAndTime.Hour (DateTime `TimeValue`)|Hour()||
|Microsoft.VisualBasic.DateAndTime.Minute (DateTime `TimeValue`)|Minute()||
|Microsoft.VisualBasic.DateAndTime.Second (DateTime `TimeValue`)|Second()||

## <a name="systemdatetime-method-instance-mapping"></a>Mapear de método System.DateTime (instância)

|Método de instância System.DateTime ()|Função canônica|
|-----------------------------------------|------------------------|
|Iguais booleanas (DateTime `value`)|Operador =|
|Dia|Dia (`this`)|
|Hora|Hora (`this`)|
|Milissegundos|Milissegundos (`this`)|
|Minuto|Minuto (`this`)|
|Mês|Mês (`this`)|
|Segundo|Segundo (`this`)|
|Year|Ano (`this`)|

## <a name="systemdatetimeoffset-method-instance-mapping"></a>Mapear o método de instância System.DateTimeOffset ()

O mapeamento mostrado para os métodos de `get` nas propriedades listadas.

|Método de instância System.DateTimeOffset ()|Função canônica|Observações|
|-----------------------------------------------|------------------------|-----------|
|Dia|Dia (`this`)|Não suportado no SQL Server 2005.|
|Hora|Hora (`this`)|Não suportado no SQL Server 2005.|
|Milissegundos|Milissegundos (`this`)|Não suportado no SQL Server 2005.|
|Minuto|Minuto (`this`)|Não suportado no SQL Server 2005.|
|Mês|Mês (`this`)|Não suportado no SQL Server 2005.|
|Segundo|Segundo (`this`)|Não suportado no SQL Server 2005.|
|Year|Ano (`this`)|Não suportado no SQL Server 2005.|

> [!NOTE]
> O método de <xref:System.DateTimeOffset.Equals%2A> retorna `true` se os objetos comparados de <xref:System.DateTimeOffset> são iguais; `false` de outra maneira. O método de <xref:System.DateTimeOffset.CompareTo%2A> retorna 0, 1 ou -1, dependendo se o objeto comparado de <xref:System.DateTimeOffset> é igual, maior do que, ou menor que, respectivamente.

## <a name="systemdatetimeoffset-method-static-mapping"></a>Mapear de método System.DateTimeOffset (estático)

O mapeamento mostrado para os métodos de `get` nas propriedades listadas.

|Método de System.DateTimeOffset (estático)|Função canônica|Observações|
|---------------------------------------------|------------------------|-----------|
|System.DateTimeOffset.Now()|CurrentDateTimeOffset()|Não suportado no SQL Server 2005.|

## <a name="systemtimespan-method-instance-mapping"></a>Mapear o método de instância System.TimeSpan ()

O mapeamento mostrado para os métodos de `get` nas propriedades listadas.

|Método de instância System.TimeSpan ()|Função canônica|Observações|
|-----------------------------------------|------------------------|-----------|
|Horas|Hora (`this`)|Não suportado no SQL Server 2005.|
|Milissegundos|Milissegundos (`this`)|Não suportado no SQL Server 2005.|
|minutos|Minuto (`this`)|Não suportado no SQL Server 2005.|
|Segundos|Segundo (`this`)|Não suportado no SQL Server 2005.|

> [!NOTE]
> O método de <xref:System.TimeSpan.Equals%2A> retorna `true` se os objetos comparados de <xref:System.TimeSpan> são iguais; `false` de outra maneira. O método de <xref:System.TimeSpan.CompareTo%2A> retorna 0, 1 ou -1, dependendo se o objeto comparado de <xref:System.TimeSpan> é igual, maior do que, ou menor que, respectivamente.

### <a name="datepart-function"></a>Função DatePart

A função de `DatePart` é mapeada a uma das várias funções canônicas diferentes, dependendo do valor de `Interval`. A tabela a seguir exibe o mapeamento canônico de função para os valores de `Interval`suportados:

|Range value|Função canônica|
|--------------------|------------------------|
|DateInterval.Year|Year()|
|DateInterval.Month|Month()|
|DateInterval.Day|Day()|
|DateInterval.Hour|Hour()|
|DateInterval.Minute|Minute()|
|DateInterval.Second|Second()|

## <a name="mathematical-function-mapping"></a>Mapeamento de função matemática

|Método CLR|Função canônica|
|----------------|------------------------|
|System.Decimal.Ceiling `d`(decimal)|Teto (`d`)|
|System.Decimal.Floor `d`(decimal)|Andar (`d`)|
|System.Decimal.Round `d`(decimal)|Redondo (`d`)|
|System.Math.Ceiling `d`(decimal)|Teto (`d`)|
|System.Math.Floor `d`(decimal)|Andar (`d`)|
|System.Math.Round `d`(decimal)|Redondo (`d`)|
|System.Math.Ceiling ( `a`dupla)|Teto (`a`)|
|System.Math.Floor ( `a`dupla)|Andar (`a`)|
|System.Math.Round ( `a`dupla)|Redondo (`a`)|
|Dígitos System.Math.Round (valor double, Int16)|Redondo (valor, dígitos)|
|Dígitos System.Math.Round (valor double, Int32)|Redondo (valor, dígitos)|
|Dígitos System.Math.Round (valor decimal, Int16)|Redondo (valor, dígitos)|
|System.Math.Round (valor decimal, Int32, dígitos)|Redondo (valor, dígitos)|
|System.Math.Abs (valor Int16)|Abs (valor)|
|System.Math.Abs (valor Int32)|Abs (valor)|
|System.Math.Abs (valor Int64)|Abs (valor)|
|System.Math.Abs (valor do byte)|Abs (valor)|
|System.Math.Abs (escolha o valor)|Abs (valor)|
|System.Math.Abs (o valor double)|Abs (valor)|
|System.Math.Abs (valor decimal)|Abs (valor)|
|System.Math.Truncate (o valor double, os dígitos Int16)|Truncar (valor, dígitos)|
|System.Math.Truncate (dobram o valor Int32, os dígitos)|Truncar (valor, dígitos)|
|Dígitos System.Math.Truncate (valor decimal, Int16)|Truncar (valor, dígitos)|
|Dígitos System.Math.Truncate (valor decimal, Int32)|Truncar (valor, dígitos)|
|Expoente System.Math.Power (valor Int32, Int64)|Põe (valor, expoente)|
|System.Math.Power (valor Int32, expoente dupla)|Põe (valor, expoente)|
|System.Math.Power (valor Int32, expoente decimal)|Põe (valor, expoente)|
|Expoente System.Math.Power (valor Int64, Int64)|Põe (valor, expoente)|
|System.Math.Power (valor Int64, expoente dupla)|Põe (valor, expoente)|
|System.Math.Power (valor Int64, expoente decimal)|Põe (valor, expoente)|
|Expoente System.Math.Power (valor double, Int64)|Põe (valor, expoente)|
|System.Math.Power (valor double, expoente dupla)|Põe (valor, expoente)|
|System.Math.Power (valor double, decimal expoente)|Põe (valor, expoente)|
|Expoente System.Math.Power (valor decimal, Int64)|Põe (valor, expoente)|
|System.Math.Power (valor decimal, expoente dupla)|Põe (valor, expoente)|
|System.Math.Power (valor decimal, expoente decimal)|Põe (valor, expoente)|

## <a name="bitwise-operator-mapping"></a>Mapeamento bit a bit de operador

|Operador bit a bit|Função canônica para operandos não booleanas|Função canônica para operandos booleanas|
|----------------------|--------------------------------------------------|---------------------------------------------|
|Operador bitwise AND|BitWiseAnd|op1 AND op2|
|Operador OR bit a bit|BitWiseOr|op1 OR op2|
|Operador bitwise NOT|BitWiseNot|NOT(op)|
|Operador bitwise XOR|BitWiseXor|((op1 AND NOT(op2)) OR (NOT(op1) AND op2))|

## <a name="other-mapping"></a>Outro mapeamento

|Método|Função canônica|
|------------|------------------------|
|Guid.NewGuid()|NewGuid()|

## <a name="see-also"></a>Consulte também

- [LINQ to Entities](linq-to-entities.md)
