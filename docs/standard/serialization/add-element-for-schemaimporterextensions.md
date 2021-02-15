---
title: Elemento <add> para <schemaImporterExtensions>
description: O <add> elemento Adiciona tipos usados pela classe XmlSchemaImporter para mapear tipos XSD para tipos .net.
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- <add> element for <schemaImporterExtensions> element
ms.assetid: c828a558-094b-441e-9065-790b87315fa0
ms.openlocfilehash: b8a0775e9d33d59606b1150aa9a1b3b1026d4b0b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726438"
---
# <a name="add-element-for-schemaimporterextensions"></a>Elemento \<add> para \<schemaImporterExtensions>

Adiciona tipos usados pelo <xref:System.Xml.Serialization.XmlSchemaImporter> para mapear tipos XSD para tipos .net. Para obter mais informações sobre arquivos de configuração, consulte [Esquema de arquivos de configuração](../../framework/configure-apps/file-schema/index.md).  
  
\<configuration>  
\<system.xml.serialization>  
\<schemaImporterExtensions>  
\<add>  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<add name = "typeName" type="fully qualified type [,Version=version number] [,Culture=culture] [,PublicKeyToken= token]"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**name**|Um nome simples que é usado para localizar a instância.|  
|**tipo**|Obrigatórios. Especifica a classe de extensão de esquema para adicionar. O valor de atributo **type** deve ser uma linha e incluir o nome do tipo totalmente qualificado. Quando o assembly é colocado no GAC (cache de assembly global), ele também deve incluir a versão, cultura e token de chave pública do assembly assinado.|  
  
### <a name="child-elements"></a>Elementos filho  

 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|DESCRIÇÃO|  
|-------------|-----------------|  
|\<schemaImporterExtensions>|Contém tipos que são usados pela <xref:System.Xml.Serialization.XmlSchemaImporter>.|  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir adiciona um tipo de extensão que o XmlSchemaImporter pode usar ao mapear tipos.  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <schemaImporterExtensions>  
       <add name="contoso" type="System.Web.Mobile.MobileCapabilities,
       System.Web.Mobile, Version=2.0.0.0, Culture=neutral,
       PublicKeyToken=b03f5f7f11d50a3a" />
    </schemaImporterExtensions>  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- [\<system.xml.serialization> Elementos](system-xml-serialization-element.md)
- [\<schemaImporterExtensions> Elementos](schemaimporterextensions-element.md)
