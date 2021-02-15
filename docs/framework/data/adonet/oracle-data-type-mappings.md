---
description: 'Saiba mais sobre: mapeamentos de tipo de dados Oracle'
title: Mapeamentos de tipo de dados Oracle
ms.date: 03/30/2017
ms.assetid: ec34ae21-bbbb-4adb-b672-83865e2a8451
ms.openlocfilehash: 1b5a130916a54049518b8b335fbf384d99035090
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754362"
---
# <a name="oracle-data-type-mappings"></a>Mapeamentos de tipo de dados Oracle

A tabela a seguir lista os tipos de dados Oracle e seus mapeamentos para o <xref:System.Data.OracleClient.OracleDataReader>.  
  
|Tipo de dados de Oracle|Tipo de dados do .NET Framework retornado por OracleDataReader.GetValue|Tipo de dados OracleClient retornado por OracleDataReader.GetOracleValue|Comentários|  
|----------------------|--------------------------------------------------------------------|------------------------------------------------------------------------|-------------|  
|**BFILE**|**Byte []**|<xref:System.Data.OracleClient.OracleBFile>||  
|**BLOB**|**Byte []**|<xref:System.Data.OracleClient.OracleLob>||  
|**CHAR**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleString>||  
|**CLOB**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleLob>||  
|**DATE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**FLOAT**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|Esse tipo de dados é um alias para o tipo de dados **Number** e é projetado para que o <xref:System.Data.OracleClient.OracleDataReader> retorne um **System. decimal** ou <xref:System.Data.OracleClient.OracleNumber> em vez de um valor de ponto flutuante. O uso do tipo de dados do .NET Framework pode causar um estouro.|  
|**INTEGER**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|Esse tipo de dados é um alias para o tipo de dados **Number (38)** e é projetado para que o <xref:System.Data.OracleClient.OracleDataReader> retorne um **System. decimal** ou <xref:System.Data.OracleClient.OracleNumber> em vez de um valor inteiro. O uso do tipo de dados do .NET Framework pode causar um estouro.|  
|**INTERVAL YEAR TO MONTH**|**Int32**|<xref:System.Data.OracleClient.OracleMonthSpan>||  
|**INTERVAL DAY TO SECOND**|**TimeSpan**|<xref:System.Data.OracleClient.OracleTimeSpan>||  
|**LONG**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleString>||  
|**LONG RAW**|**Byte []**|<xref:System.Data.OracleClient.OracleBinary>||  
|**NCHAR**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleString>||  
|**NCLOB**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleLob>||  
|**AUTOMÁTICA**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|O uso do tipo de dados do .NET Framework pode causar um estouro.|  
|**NVARCHAR2**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleString>||  
|**RAW**|**Byte []**|<xref:System.Data.OracleClient.OracleBinary>||  
|**REF CURSOR**|||O tipo de dados **cursor de referência** do Oracle não é suportado pelo <xref:System.Data.OracleClient.OracleDataReader> objeto.|  
|**ROWID**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleString>||  
|**TIMESTAMP**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**TIMESTAMP WITH LOCAL TIME ZONE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**TIMESTAMP WITH TIME ZONE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**INTEIRO SEM SINAL**|**Número**|<xref:System.Data.OracleClient.OracleNumber>|Esse tipo de dados é um alias para o tipo de dados **Number (38)** e é projetado para que o <xref:System.Data.OracleClient.OracleDataReader> retorne um **System. decimal** ou <xref:System.Data.OracleClient.OracleNumber> em vez de um valor inteiro sem sinal. O uso do tipo de dados do .NET Framework pode causar um estouro.|  
|**VARCHAR2**|**Cadeia de caracteres**|<xref:System.Data.OracleClient.OracleString>||  
  
 A tabela a seguir lista os tipos de dados do Oracle e os tipos de dados .NET Framework (**System. Data. DbType** e <xref:System.Data.OracleClient.OracleType> ) a serem usados ao associá-los como parâmetros.  
  
|Tipo de dados de Oracle|Enumeração DbType a ser associada como um parâmetro|Enumeração OracleType a ser associada como um parâmetro|Comentários|  
|----------------------|-----------------------------------------------|---------------------------------------------------|-------------|  
|**BFILE**||**BArquivo**|O Oracle só permite a associação de um **bArquivo** como um parâmetro **bArquivo** . O .NET Provedor de Dados para Oracle não construirá um automaticamente para você se você tentar associar um valor não **bArquivo** , como **byte []** ou <xref:System.Data.OracleClient.OracleBinary> .|  
|**BLOB**||**Blob**|O Oracle só permite a associação de um **blob** como um parâmetro de **blob** . O .NET Provedor de Dados para Oracle não construirá um automaticamente para você se você tentar associar um valor não-**blob** , como **byte []** ou <xref:System.Data.OracleClient.OracleBinary> .|  
|**CHAR**|**AnsiStringFixedLength**|**Char**||  
|**CLOB**||**CLOB**|O Oracle só permite a vinculação de um **CLOB** como um parâmetro **CLOB** . O .NET Provedor de Dados para Oracle não construirá um automaticamente para você se você tentar associar um valor não **CLOB** , como **System. String** ou <xref:System.Data.OracleClient.OracleString> .|  
|**DATE**|**DateTime**|**DateTime**||  
|**FLOAT**|**Único, duplo, decimal**|**Float, Double, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> determina o **System. Data. DbType** e o <xref:System.Data.OracleClient.OracleType> .|  
|**INTEGER**|**SByte, Int16, Int32, Int64, Decimal**|**SByte, Int16, Int32, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> determina o **System. Data. DbType** e o <xref:System.Data.OracleClient.OracleType> .|  
|**INTERVAL YEAR TO MONTH**|**Int32**|**IntervalYearToMonth**|<xref:System.Data.OracleClient.OracleType> só está disponível com o uso do software cliente e servidor Oracle 9i.|  
|**INTERVAL DAY TO SECOND**|**Objeto**|**IntervalDayToSecond**|<xref:System.Data.OracleClient.OracleType> só está disponível com o uso do software cliente e servidor Oracle 9i.|  
|**LONG**|**AnsiString**|**LongVarChar**||  
|**LONG RAW**|**Binary**|**LongRaw**||  
|**NCHAR**|**StringFixedLength**|**NChar**||  
|**NCLOB**||**NClob**|O Oracle só permite a vinculação de um **NClob** como um parâmetro **NClob** . O .NET Provedor de Dados para Oracle não construirá um automaticamente para você se você tentar associar um valor não **NClob** , como **System. String** ou <xref:System.Data.OracleClient.OracleString> .|  
|**AUTOMÁTICA**|**VarNumeric**|**Número**||  
|**NVARCHAR2**|**Cadeia de caracteres**|**NVarChar**||  
|**RAW**|**Binary**|**Bruta**||  
|**REF CURSOR**||**Cursor**|Para obter mais informações, consulte [cursores de referência do Oracle](oracle-ref-cursors.md).|  
|**ROWID**|**AnsiString**|**ROWID**||  
|**TIMESTAMP**|**DateTime**|**Timestamp**|<xref:System.Data.OracleClient.OracleType> só está disponível com o uso do software cliente e servidor Oracle 9i.|  
|**TIMESTAMP WITH LOCAL TIME ZONE**|**DateTime**|**TimestampLocal**|<xref:System.Data.OracleClient.OracleType> só está disponível com o uso do software cliente e servidor Oracle 9i.|  
|**TIMESTAMP WITH TIME ZONE**|**DateTime**|**TimestampWithTz**|<xref:System.Data.OracleClient.OracleType> só está disponível com o uso do software cliente e servidor Oracle 9i.|  
|**INTEIRO SEM SINAL**|**Byte, UInt16, UInt32, UInt64, Decimal**|**Byte, UInt16, Uint32, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> determina o **System. Data. DbType** e o <xref:System.Data.OracleClient.OracleType> .|  
|**VARCHAR2**|**AnsiString**|**VarChar**||  
  
 Os valores de **parameterdirectity** **InputOutput**, **output** e **ReturnValue** usados pela <xref:System.Data.OracleClient.OracleParameter.Value%2A> Propriedade do <xref:System.Data.OracleClient.OracleParameter> objeto são .NET Framework tipos de dados, a menos que o valor de entrada seja um tipo de dados Oracle (por exemplo, <xref:System.Data.OracleClient.OracleNumber> ou <xref:System.Data.OracleClient.OracleString> ). Isso não se aplica aos tipos de dados **cursor de referência**, **bArquivo** ou **LOB** .  
  
## <a name="see-also"></a>Consulte também

- [Oracle e ADO.NET](oracle-and-adonet.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
