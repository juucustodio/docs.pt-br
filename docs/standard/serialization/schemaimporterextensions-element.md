---
title: Elemento <schemaImporterExtensions>
description: O <schemaImporterExtensions> elemento contém tipos que são usados pelo XmlSchemaImporter para mapeamento de tipos XSD para tipos .net.
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- schemaImporterExtensions element
- <schemaImporterExtensions> element
ms.assetid: 465ef2a0-f909-4ac1-9a56-0ead5c849698
ms.openlocfilehash: 6b644ed1112b748be4dd301d6fa6f2a6416dc67e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722135"
---
# <a name="schemaimporterextensions-element"></a>Elemento \<schemaImporterExtensions>

Contém tipos que são usados pelo <xref:System.Xml.Serialization.XmlSchemaImporter> para mapeamento de tipos XSD para tipos .net. Para obter mais informações sobre arquivos de configuração, consulte [Esquema de arquivos de configuração](../../framework/configure-apps/file-schema/index.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<schemaImporterExtensions>  
    <!-- Add types -->  
</schemaImporterExtensions>  
```  
  
## <a name="child-elements"></a>Elementos filho  
  
|Elemento|DESCRIÇÃO|  
|-------------|-----------------|  
|[\<add> Elemento para \<schemaImporterExtensions>](add-element-for-schemaimporterextensions.md)|Adiciona tipos que são usados pela <xref:System.Xml.Serialization.XmlSchemaImporter> para criar mapeamentos.|  
  
## <a name="parent-elements"></a>Elementos pai  
  
|Elemento|DESCRIÇÃO|  
|-------------|-----------------|  
|[\<system.xml.serialization> Elementos](system-xml-serialization-element.md)|O elemento de nível superior para controlar a serialização XML.|  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir ilustra como adicionar tipos que são usados pelo <xref:System.Xml.Serialization.XmlSchemaImporter> ao mapear tipos XSD para tipos .net.  
  
```xml  
<system.xml.serialization>  
    <schemaImporterExtensions>  
        <add name = "MobileCapabilities" type =
        "System.Web.Mobile.MobileCapabilities,
        System.Web.Mobile, Version - 2.0.0.0, Culture = neutral,
        PublicKeyToken = b03f5f6f11d40a3a" />  
    </schemaImporterExtensions>  
</system.xml.serialization>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>
- [Esquema do arquivo de configuração](../../framework/configure-apps/file-schema/index.md)
- [\<dateTimeSerialization> Elementos](datetimeserialization-element.md)
- [\<add> Elemento para \<schemaImporterExtensions>](add-element-for-schemaimporterextensions.md)
- [\<system.xml.serialization> Elementos](system-xml-serialization-element.md)
