---
description: 'Saiba mais sobre: OLE DB mapeamentos de tipo de dados'
title: Mapeamentos de tipo de dados do OLE DB
ms.date: 03/30/2017
ms.assetid: 04bcb259-59d3-4fd7-894d-4f0dd0c68069
ms.openlocfilehash: 8dd750754a67921437ca9b8fac751857961385cc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786180"
---
# <a name="ole-db-data-type-mappings"></a>Mapeamentos de tipo de dados do OLE DB

A tabela a seguir mostra o tipo de .NET Framework inferido para tipos de dados do .NET Framework Provedor de Dados para ADO e OLE DB ( <xref:System.Data.OleDb> ). Os métodos de acessadores tipados para o <xref:System.Data.OleDb.OleDbDataReader> também são listados.  
  
|Tipo de ADO|Tipo OLE DB|Tipo de .NET Framework|Acessador .NET Framework tipado|  
|--------------|-----------------|----------------------------------------------------------------------|--------------------------------------------------------------------------------|  
|adBigInt|DBTYPE_I8|Int64|GetInt64 ()|  
|adBinary|DBTYPE_BYTES|Byte[]|GetBytes ()|  
|adBoolean|DBTYPE_BOOL|Boolean|GetBoolean ()|  
|adBSTR|DBTYPE_BSTR|String|GetString ()|  
|adChapter|DBTYPE_HCHAPTER|Com suporte por meio do `DataReader` . Consulte [recuperando dados usando um DataReader](retrieving-data-using-a-datareader.md).|GetValue ()|  
|adChar|DBTYPE_STR|String|GetString ()|  
|adCurrency|DBTYPE_CY|Decimal|GetDecimal ()|  
|adDate|DBTYPE_DATE|DateTime|GetDateTime ()|  
|adDBDate|DBTYPE_DBDATE|DateTime|GetDateTime ()|  
|adDBTime|DBTYPE_DBTIME|DateTime|GetDateTime ()|  
|adDBTimeStamp|DBTYPE_DBTIMESTAMP|DateTime|GetDateTime ()|  
|adDecimal|DBTYPE_DECIMAL|Decimal|GetDecimal ()|  
|adDouble|DBTYPE_R8|Double|GetDouble ()|  
|adError|DBTYPE_ERROR|ExternalException|GetValue ()|  
|adFileTime|DBTYPE_FILETIME|DateTime|GetDateTime ()|  
|adGUID|DBTYPE_GUID|Guid|GetGuid ()|  
|adIDispatch|DBTYPE_IDISPATCH *|Objeto|GetValue ()|  
|adInteger|DBTYPE_I4|Int32|GetInt32 ()|  
|adIUnknown|DBTYPE_IUNKNOWN *|Objeto|GetValue ()|  
|adNumeric|DBTYPE_NUMERIC|Decimal|GetDecimal ()|  
|adPropVariant|DBTYPE_PROPVARIANT|Objeto|GetValue ()|  
|adSingle|DBTYPE_R4|Single|GetFloat ()|  
|adSmallInt|DBTYPE_I2|Int16|GetInt16 ()|  
|adTinyInt|DBTYPE_I1|Byte|GetByte ()|  
|adUnsignedBigInt|DBTYPE_UI8|UInt64|GetValue ()|  
|adUnsignedInt|DBTYPE_UI4|UInt32|GetValue ()|  
|adUnsignedSmallInt|DBTYPE_UI2|UInt16|GetValue ()|  
|adUnsignedTinyInt|DBTYPE_UI1|Byte|GetByte ()|  
|adVariant|DBTYPE_VARIANT|Objeto|GetValue ()|  
|adWChar|DBTYPE_WSTR|String|GetString ()|  
|adUserDefined|DBTYPE_UDT|sem suporte||  
|adVarNumeric|DBTYPE_VARNUMERIC|sem suporte||  
  
 \* Para os tipos de OLE DB `DBTYPE_IUNKNOWN` e `DBTYPE_IDISPATCH` , a referência de objeto é uma representação empacotada do ponteiro.  
  
## <a name="see-also"></a>Confira também

- [Recuperando e modificando dados no ADO.NET](retrieving-and-modifying-data.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
