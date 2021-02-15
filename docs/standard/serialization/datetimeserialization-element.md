---
title: Elemento <dateTimeSerialization>
description: Este artigo descreve o <dateTimeSerialization> elemento, que determina o modo de serialização de objetos DateTime.
ms.date: 03/30/2017
helpviewer_keywords:
- dateTimeSerialization element
- XML serialization, configuration
- <dateTimeSerialization> element
ms.assetid: 90fda55c-7730-41e9-bc4b-6423a4b920af
ms.openlocfilehash: 1623517e66955c14b7e738c860ec16086fe30429
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95678968"
---
# <a name="datetimeserialization-element"></a>Elemento \<dateTimeSerialization>

Determina o modo de serialização de objetos <xref:System.DateTime>.  
  
 \<configuration>  
\<dateTimeSerialization>  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<dateTimeSerialization  
    mode = "Roundtrip|Local"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributos|Descrição|  
|----------------|-----------------|  
|`mode`|Opcional. Especifica o modo de serialização. Define como um dos valores de <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>. O padrão é **RoundTrip**.|  
  
### <a name="child-elements"></a>Elementos filho  

 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|DESCRIÇÃO|  
|-------------|-----------------|  
|system.xml.serialization|O elemento de nível superior para controlar a serialização XML.|  
  
## <a name="remarks"></a>Comentários  

Quando essa propriedade é definida como **local**, <xref:System.DateTime> os objetos são sempre formatados como a hora local. Ou seja, as informações de fuso horário local são sempre incluídas com os dados serializados.
  
Quando essa propriedade é definida como de **ida e volta**, os <xref:System.DateTime> objetos são examinados para determinar se estão no local, no UTC ou em um fuso horário não especificado. Os objetos <xref:System.DateTime> são então serializados de modo que essas informações sejam preservadas. Esse é o comportamento padrão recomendado para todos os novos aplicativos que não se comunicam com versões antigas do framework.  
  
## <a name="see-also"></a>Confira também

- <xref:System.DateTime>
- <xref:System.Xml.Serialization.XmlSchemaImporter>
- <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>
- [Esquema do arquivo de configuração](../../framework/configure-apps/file-schema/index.md)
- [\<schemaImporterExtensions> Elementos](schemaimporterextensions-element.md)
- [\<add> Elemento para \<schemaImporterExtensions>](add-element-for-schemaimporterextensions.md)
- [\<system.xml.serialization> Elementos](system-xml-serialization-element.md)
