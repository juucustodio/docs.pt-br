---
description: 'Saiba mais sobre: XmlDictionaryReaderQuotas'
title: XmlDictionaryReaderQuotas
ms.date: 03/30/2017
ms.assetid: 9b4ca8b4-0a89-4758-97ab-528a8ce18f07
ms.openlocfilehash: d1450051e7107e9b92f848d26e6b182bfd2f2340
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756858"
---
# <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas

XmlDictionaryReaderQuotas  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class XmlDictionaryReaderQuotas  
{  
  sint32 MaxArrayLength;  
  sint32 MaxBytesPerRead;  
  sint32 MaxDepth;  
  sint32 MaxNameTableCharCount;  
  sint32 MaxStringContentLength;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe XmlDictionaryReaderQuotas não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe XmlDictionaryReaderQuotas tem as seguintes propriedades:  
  
### <a name="maxarraylength"></a>MaxArrayLength  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 A extensão máxima permitida da matriz.  
  
### <a name="maxbytesperread"></a>MaxBytesPerRead  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O máximo de bytes permitidos retornados para cada leitura.  
  
### <a name="maxdepth"></a>MaxDepth  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 A profundidade máxima do nó aninhado para cada leitura.  
  
### <a name="maxnametablecharcount"></a>MaxNameTableCharCount  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O máximo de caracteres permitidos no nome da tabela.  
  
### <a name="maxstringcontentlength"></a>MaxStringContentLength  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O máximo de caracteres permitidos no conteúdo do elemento XML.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.Xml.XmlDictionaryReaderQuotas>
- <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>
