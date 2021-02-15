---
description: 'Saiba mais sobre: SqlClient para Entity FrameworkTypes'
title: SqlClient para a entidade FrameworkTypes
ms.date: 03/30/2017
ms.assetid: f2a95ead-c845-4e97-9fb3-04b444f7ed81
ms.openlocfilehash: 92bd557198d203229394fb3a4c2fe286e217edca
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99673174"
---
# <a name="sqlclient-for-entity-frameworktypes"></a>SqlClient para a entidade FrameworkTypes

O provedor de dados. NET Framework para o arquivo de manifesto do provedor SQL Server (SqlClient) inclui a lista de tipos primitivos de provedor, de facetas para cada tipo, de mapeamento entre os tipos primitivos e modelo conceitual de armazenamento, e regras da promoção e de conversão entre os tipos primitivos modelo conceitual e do armazenamento.  
  
 A tabela a seguir descreve os tipos de SQL Server 2008, SQL Server 2005 e SQL Server bancos de dados do 2000 e como esses tipos são mapeados para tipos de modelo conceitual. Alguns novos tipos foram introduzidos em versões posteriores do SQL Server não são suportados nas versões anteriores do SQL Server. Esses tipos são observados na tabela abaixo.  
  
|Tipo de provedor<br /><br /> name|Tipo de provedor<br /><br /> Atributos|`EDMSimpleType`<br /><br /> name|Facetas|  
|----------------------------|----------------------------------|------------------------------|------------|  
|`bit`|n/a|`Edm.Boolean`|n/a|  
|`tinyint`|n/a|`Edm.Byte`|n/a|  
|`smallint`|n/a|`Edm.Int16`|n/a|  
|`int`|n/a|`Edm.Int32`|n/a|  
|`bigint`|n/a|`Edm.Int64`|n/a|  
|`float`|n/a|`Edm.Double`|n/a|  
|`real`|n/a|`Edm.Double`|n/a|  
|`decimal`|n/a|`Edm.Decimal`|Preciso<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 38<br /><br /> -Padrão: 18<br /><br /> -Constante: false<br /><br /> Escala:<br /><br /> -Mínimo: 0<br /><br /> -Máximo: 38<br /><br /> -Padrão: 0<br /><br /> -Constante: false|  
|`numeric`|n/a|`Edm.Decimal`|Preciso<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 38<br /><br /> -Padrão: 18<br /><br /> -Constante: false<br /><br /> Escala:<br /><br /> -Mínimo: 0<br /><br /> -Máximo: 38<br /><br /> -Padrão: 0<br /><br /> -Constante: false|  
|`smallmoney`|n/a|`Edm.Decimal`|Preciso<br /><br /> -Padrão: 10<br /><br /> -Constante: true<br /><br /> Escala:<br /><br /> -Padrão: 4<br /><br /> -Constante: true|  
|`money`|n/a|`Edm.Decimal`|Preciso<br /><br /> -Padrão: 19<br /><br /> -Constante: true<br /><br /> Escala:<br /><br /> -Padrão: 4<br /><br /> -Constante: true|  
|`binary`|n/a|`Edm.Binary`|Determinado<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 8000<br /><br /> -Padrão: 8000<br /><br /> -Constante: false<br /><br /> Cadeia<br /><br /> -Padrão: true<br /><br /> -Constante: true|  
|`varbinary`|n/a|`Edm.Binary`|Determinado<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 8000<br /><br /> -Padrão: 8000<br /><br /> -Constante: false<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`varbinary(max)`<br /><br /> Observação: esse tipo não tem suporte no SQL Server 2000.|n/a|`Edm.Binary`|Determinado<br /><br /> -Padrão: 214748364780<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`image`|n/a|`Edm.Binary`|Determinado<br /><br /> -Padrão: 2147483647<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`timestamp`|n/a|`Edm.Binary`|Determinado<br /><br /> -Padrão: 8<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: true<br /><br /> -Constante: true|  
|`rowversion`|n/a|`Edm.Binary`|Determinado<br /><br /> -Padrão: 8<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: true<br /><br /> -Constante: true|  
|`smalldatetime`|n/a|`Edm.DateTime`|Preciso<br /><br /> -Padrão: 0<br /><br /> -Constante: true|  
|`datetime`|n/a|`Edm.DateTime`|Preciso<br /><br /> -Padrão: 3<br /><br /> -Constante: true|  
|`date`<br /><br /> Observação: esse tipo não tem suporte no SQL Server 2005 e SQL Server 2000.|n/a|`Edm.DateTime`|Preciso<br /><br /> -Padrão: 0<br /><br /> -Constante: false|  
|`time`<br /><br /> Observação: esse tipo não tem suporte no SQL Server 2005 e SQL Server 2000.|n/a|`Edm.Time`|Preciso<br /><br /> -Padrão: 7<br /><br /> -Constante: false|  
|`datetime2`<br /><br /> Observação: esse tipo não tem suporte no SQL Server 2005 e SQL Server 2000.|n/a|`Edm.DateTime`|Preciso<br /><br /> -Padrão: 7<br /><br /> -Constante: false|  
|`datetimeoffset`<br /><br /> Observação: esse tipo não tem suporte no SQL Server 2005 e SQL Server 2000.|n/a|`Edm.DateTimeOffset`|Preciso<br /><br /> -Padrão: 7<br /><br /> -Constante: false|  
|`nvarchar`<br /><br /> Observação: esse tipo não tem suporte no SQL Server 2000.|n/a|`Edm.String`|Determinado<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 4000<br /><br /> -Padrão: 4000<br /><br /> -Constante: false<br /><br /> Unicode:<br /><br /> -Padrão: true<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`varchar`<br /><br /> Observação: esse tipo não tem suporte no SQL Server 2000.|n/a|`Edm.String`|Determinado<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 8000<br /><br /> -Padrão: 8000<br /><br /> -Constante: false<br /><br /> Unicode:<br /><br /> -Padrão: false<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`char`|n/a|`Edm.String`|Determinado<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 8000<br /><br /> -Padrão: 8000<br /><br /> -Constante: false<br /><br /> Unicode:<br /><br /> -Padrão: false<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: true<br /><br /> -Constante: true|  
|`nchar`|n/a|`Edm.String`|Determinado<br /><br /> -Mínimo: 1<br /><br /> -Máximo: 4000<br /><br /> -Padrão: 4000<br /><br /> -Constante: false<br /><br /> Unicode:<br /><br /> -Padrão: true<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: true<br /><br /> -Constante: true|  
|`varchar`(`max`)|n/a|`Edm.String`|Determinado<br /><br /> -Padrão: 2147483647<br /><br /> -Constante: true<br /><br /> Unicode:<br /><br /> -Padrão: false<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`nvarchar`(`max`)|n/a|`Edm.String`|Determinado<br /><br /> -Padrão: 1073741823<br /><br /> -Constante: true<br /><br /> Unicode:<br /><br /> -Padrão: true<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`ntext`|Igual comparável: falso<br /><br /> Ordem comparável: falso|`Edm.String`|Determinado<br /><br /> -Padrão: 1073741823<br /><br /> -Constante: true<br /><br /> Unicode:<br /><br /> -Padrão: false<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`text`|Igual comparável: falso<br /><br /> Ordem comparável: falso|`Edm.String`|Determinado<br /><br /> -Padrão: 2147483647<br /><br /> -Constante: true<br /><br /> Unicode:<br /><br /> -Padrão: false<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
|`Unique`<br /><br /> `identifier`|Igual comparável: verdadeiro<br /><br /> Ordem comparável: true|`Edm.Guid`|n/a|  
|`xml`|Igual comparável: falso<br /><br /> Ordem comparável: falso|`Edm.String`|Determinado<br /><br /> -Padrão: 1073741823<br /><br /> -Constante: true<br /><br /> Unicode:<br /><br /> -Padrão: true<br /><br /> -Constante: true<br /><br /> Cadeia<br /><br /> -Padrão: false<br /><br /> -Constante: true|  
  
## <a name="see-also"></a>Consulte também

- [Especificações de CSDL, SSDL e MSL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
