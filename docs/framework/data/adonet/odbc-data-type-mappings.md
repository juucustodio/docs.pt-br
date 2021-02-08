---
description: 'Saiba mais sobre: mapeamentos de tipo de dados ODBC'
title: Mapeamentos de tipo de dados ODBC
ms.date: 03/30/2017
ms.assetid: 43c35d32-831d-480f-a150-78f7e869d17f
ms.openlocfilehash: 0589f065da852158d35ee1104618dd13e5b2d36f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786206"
---
# <a name="odbc-data-type-mappings"></a>Mapeamentos de tipo de dados ODBC

A tabela a seguir mostra o tipo de .NET Framework inferido para tipos de dados do .NET Framework Provedor de Dados para ODBC ( <xref:System.Data.Odbc> ). Os métodos de acessadores tipados para o <xref:System.Data.Odbc.OdbcDataReader> também são listados.  
  
|Tipo de ODBC|Tipo de .NET Framework|Acessador .NET Framework tipado|  
|---------------|----------------------------------------------------------------------|--------------------------------------------------------------------------------|  
|SQL_BIGINT|Int64|GetInt64 ()|  
|SQL_BINARY|Byte[]|GetBytes ()|  
|SQL_BIT|Boolean|GetBoolean ()|  
|SQL_CHAR|String<br /><br /> Char[]|GetString ()<br /><br /> GetChars ()|  
|SQL_DECIMAL|Decimal|GetDecimal ()|  
|SQL_DOUBLE|Double|GetDouble ()|  
|SQL_GUID|Guid|GetGuid ()|  
|SQL_INTEGER|Int32|GetInt32 ()|  
|SQL_LONG_VARCHAR|String<br /><br /> Char[]|GetString ()<br /><br /> GetChars ()|  
|SQL_LONGVARBINARY|Byte[]|GetBytes ()|  
|SQL_NUMERIC|Decimal|GetDecimal ()|  
|SQL_REAL|Único|GetFloat ()|  
|SQL_SMALLINT|Int16|GetInt16 ()|  
|SQL_TINYINT|Byte|GetByte ()|  
|SQL_TYPE_TIMES|Datetime|GetDateTime ()|  
|SQL_TYPE_TIMESTAMP|Datetime|GetDateTime ()|  
|SQL_VARBINARY|Byte[]|GetBytes ()|  
|SQL_WCHAR|String<br /><br /> Char[]|GetString ()<br /><br /> GetChars ()|  
|SQL_WLONGVARCHAR|String<br /><br /> Char[]|GetString ()<br /><br /> GetChars ()|  
|SQL_WVARCHAR|String<br /><br /> Char[]|GetString ()<br /><br /> GetChars ()|  
  
## <a name="see-also"></a>Confira também

- [Recuperando e modificando dados no ADO.NET](retrieving-and-modifying-data.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
