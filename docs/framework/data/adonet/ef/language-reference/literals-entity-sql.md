---
description: 'Saiba mais sobre: literais (Entity SQL)'
title: Literais (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 092ef693-6e5f-41b4-b868-5b9e82928abf
ms.openlocfilehash: cae2ec7ab8cf19166dc3100a85473fca2ed0a7be
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791875"
---
# <a name="literals-entity-sql"></a>Literais (Entity SQL)

Este tópico descreve o suporte de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] para literais.  
  
## <a name="null"></a>Nulo  

 O literal nulo é usado para representar o zero valor de qualquer tipo. Um literal nulo é compatível com qualquer tipo.  
  
 Tipado anula pode ser criado por uma conversão sobre um literal nulo. Para obter mais informações, consulte [Cast](cast-entity-sql.md).  
  
 Para regras sobre onde literais nulos flutuantes livres podem ser usados, consulte [literais nulos e inferência de tipos](null-literals-and-type-inference-entity-sql.md).  
  
## <a name="boolean"></a>Boolean  

 Literais booleanos são representados pelas palavras-chave `true` e `false`.  
  
## <a name="integer"></a>Integer  

 Literais inteiro podem ser do tipo <xref:System.Int32> ou <xref:System.Int64>. Um literal de <xref:System.Int32> é uma série de caracteres numéricos. Um literal de <xref:System.Int64> é uma série de caracteres numéricos seguidos por um maiúsculas. L.  
  
## <a name="decimal"></a>Decimal  

 Número de ponto fixo (decimal) é uma série de caracteres numéricos, um ponto (.) e de outras uma série de caracteres numéricos seguidos por um maiúsculas “M”.  
  
## <a name="float-double"></a>Float, double  

 Um número de precisão dupla de ponto flutuante é uma série de caracteres numéricos, um ponto (.) e de outras uma série de caracteres numéricos possivelmente seguidos por um expoente. Um número de ponto flutuante de único precisões (ou o flutuante) são uma sintaxe de precisão dupla de números de ponto flutuante seguido pela minúsculas F.  
  
## <a name="string"></a>String  

 Uma cadeia de caracteres é uma série de caracteres incluídos em marcas de aspas. As aspas podem ser ambas as aspas simples (`'`) ou ambas as com aspas ("). Literais de cadeia de caracteres podem ser Unicode ou não Unicode. Para declarar um literal de cadeia de caracteres como Unicode, prefixe o literal com uma letra maiúscula “Em”. O padrão é literais de cadeia de caracteres de não Unicode. Não é possível que haja nenhum espaço entre o N e a carga útil do literal de cadeia de caracteres, e No deve ser maiúscula.  
  
```sql  
'hello' -- non-Unicode character string literal  
N'hello' -- Unicode character string literal  
"x"  
N"This is a string!"  
'so is THIS'  
```  
  
## <a name="datetime"></a>Datetime  

 Um literal de datetime é independente da localidade e é composto de uma parte da data e uma parte de tempo. Partes de data e hora são imperativas e não há nenhum valor padrão.  
  
 A parte de data deve ter o formato: `YYYY` - `MM` - `DD` , em que `YYYY` é um valor de ano de quatro dígitos entre 0001 e 9999, `MM` é o mês entre 1 e 12 e `DD` é o valor de dia que é válido para o mês determinado `MM` .  
  
 A parte de tempo deve ter o formato: `HH`:`MM`[:`SS`[.fffffff]], onde `HH` é o valor de hora entre 0 e 23, `MM` é minúsculo o valor entre 0 e 59, `SS` é o segundo valor entre 0 e 59 e o fffffff são o segundo valor fracionário entre 0 e 9999999. Todos os intervalos de valores são incluindo. Os segundos fracionários são opcionais. Os segundos são opcionais a menos que os segundos fracionários são especificados; nesse caso, os segundos são necessários. Quando os segundos ou os segundos fracionários não for especificado, o valor padrão de zero será usado em vez disso.  
  
 Pode haver qualquer número de espaços entre o símbolo de DATETIME e a carga útil literal, mas nenhuma novas linhas.  
  
```sql  
DATETIME'2006-10-1 23:11'  
DATETIME'2006-12-25 01:01:00.0000000' -- same as DATETIME'2006-12-25 01:01'  
```  
  
## <a name="time"></a>Hora  

 Um literal hora é independente da localidade e composta de uma parte de tempo somente. A parte de tempo é imperativa e não há nenhum valor padrão. Deve ter o formato HH:MM[:SS[.fffffff]], onde HH é o valor de hora entre 0 e 23, MM são o minuto valor entre 0 e 59, SS são o segundo valor entre 0 e 59, e fffffff é o segundo valor da fração entre 0 e 9999999. Todos os intervalos de valores são incluindo. Os segundos fracionários são opcionais. Os segundos são opcionais a menos que os segundos fracionários são especificados; nesse caso, os segundos são necessários. Quando os segundos ou frações não for especificado, o valor padrão de zero será usado em vez disso.  
  
 Pode haver qualquer número de espaços entre o símbolo de TEMPOS e a carga útil literal, mas nenhuma novas linhas.  
  
```sql  
TIME‘23:11’  
TIME‘01:01:00.1234567’  
```  
  
## <a name="datetimeoffset"></a>DateTimeOffset  

 Um literal de datetimeoffset é independente da localidade e composta de uma parte da data, uma parte de tempo, e uma parte de deslocamento. Todos datam, multiplicado por, e as partes de deslocamento são imperativas e não há nenhum valor padrão. A parte de data deve ter o formato YYYY YYYY-MM-DD, onde é um valor do ano de quatro dígitos entre 0001 e 9999, mm é o mês entre 1 e 12, e o DD é o valor do dia que é válido para o mês determinado. A parte de tempo deve ter o formato HH:MM[:SS[.fffffff]], onde HH é o valor de hora entre 0 e 23, MM são o minuto valor entre 0 e 59, SS são o segundo valor entre 0 e 59, e fffffff é o segundo valor fracionário entre 0 e 9999999. Todos os intervalos de valores são incluindo. Os segundos fracionários são opcionais. Os segundos são opcionais a menos que os segundos fracionários são especificados; nesse caso, os segundos são necessários. Quando os segundos ou frações não for especificado, o valor padrão de zero será usado em vez disso. A parte de deslocamento deve ter o formato {+&#124;-} HH: MM, em que HH e MM têm o mesmo significado que na parte de hora. O intervalo de deslocamento, no entanto, deve estar entre o 14:00 e + -14:00  
  
 Pode haver qualquer número de espaços entre o símbolo de DATETIMEOFFSET e a carga útil literal, mas nenhuma novas linhas.  
  
```sql  
DATETIMEOFFSET‘2006-10-1 23:11 +02:00’  
DATETIMEOFFSET‘2006-12-25 01:01:00.0000000 -08:30’  
```  
  
> [!NOTE]
> Um valor literal válido de Entity SQL pode cair fora dos intervalos suportados para CLR ou a fonte de dados. Isso pode levar a uma exceção  
  
## <a name="binary"></a>Binário  

 Um literal de cadeia de caracteres binário é uma sequência de dígitos hexadecimais delimitado por aspas simples que seguem binário de palavra-chave ou o símbolo `X` ou `x`de atalho. O símbolo `X` de atalho não difere maiúsculas de minúsculas. Zero ou mais espaços são permitidos entre a palavra-chave `binary` e o valor da cadeia de caracteres binário.  
  
 Os caracteres hexadecimais também são não diferencia maiúsculas de minúsculas. Se o literal é composta de um número ímpar de dígitos hexadecimais, o literal será alinhado ao mesmo dígito hexadecimal seguir prefixando o literal com um dígito hexadecimal zero. Não há um limite formal no tamanho da cadeia de caracteres binário.  
  
```sql  
Binary'00ffaabb'  
X'ABCabc'  
BINARY    '0f0f0f0F0F0F0F0F0F0F'  
X'' –- empty binary string  
```  
  
## <a name="guid"></a>Guid  

 Um literal de `GUID` representa um identificador exclusivo. É uma sequência formada pela palavra-chave `GUID` seguida por dígitos hexadecimais no formulário conhecido como formato de *registro* : 8-4-4-4-12 entre aspas simples. Os dígitos hexadecimais não diferenciam maiúsculas de minúsculas.  
  
 Pode haver qualquer número de espaços entre o símbolo de TEMPOS e a carga útil literal, mas nenhuma novas linhas.  
  
```sql  
Guid'1afc7f5c-ffa0-4741-81cf-f12eAAb822bf'  
GUID  '1AFC7F5C-FFA0-4741-81CF-F12EAAB822BF'  
```  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
