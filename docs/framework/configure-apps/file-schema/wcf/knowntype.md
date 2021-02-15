---
description: 'Saiba mais sobre: <knownType>'
title: <knownType>
ms.date: 03/30/2017
ms.assetid: ee2b7be3-7148-4a3a-b861-48e7330615e5
ms.openlocfilehash: 205f799c81263be3dd08aae9efefb975b06a0cc7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99725500"
---
# \<knownType>

Especifica um tipo a ser usado pelo <xref:System.Runtime.Serialization.DataContractSerializer> durante a desserialização. O elemento especifica um "tipo conhecido" que é retornado por um campo ou propriedade de um "tipo declarado". Para obter mais informações, consulte [tipos conhecidos de contrato de dados](../../../wcf/feature-details/data-contract-known-types.md).  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.serialization>**](system-runtime-serialization.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<dataContractSerializer>**](datacontractserializer.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<declaredTypes>**](declaredtypes.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add-of-declaredtypes-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<knownType>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<knownType type="String">
  <parameter index="Integer"
             type="String" />
</knownType>
```  
  
## <a name="type"></a>Tipo  

 `string`  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|type|Especifica o tipo (incluindo o namespace), o nome do assembly, a versão, a cultura e o token de chave pública.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<parameter>](parameter.md)|Especifica um índice de parâmetro quando o tipo declarado é um tipo genérico.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<add>](add-of-declaredtypes-element.md)|Adiciona um tipo declarado à coleção de tipos declarados.|  
  
## <a name="remarks"></a>Comentários  

 Para obter mais informações sobre tipos conhecidos, consulte [tipos conhecidos de contrato de dados](../../../wcf/feature-details/data-contract-known-types.md) e <xref:System.Runtime.Serialization.DataContractSerializer> .  
  
 Consulte o [\<dataContractSerializer>](datacontractserializer-element.md) para obter um exemplo de como usar esse elemento.  
  
## <a name="example"></a>Exemplo  
  
```xml  
<add type="MyCompany.Library.Shape,
           MyAssembly, Version=2.0.0.0, Culture=neutral,
           PublicKeyToken=XXXXXX, processorArchitecture=MSIL">
  <knownType type="MyCompany.Library.Circle,
                   MyAssembly, Version=2.0.0.0, Culture=neutral,
                   PublicKeyToken=XXXXXX,
                   processorArchitecture=MSIL"/>
</add>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [Tipos de contratos de dados conhecidos](../../../wcf/feature-details/data-contract-known-types.md)
- [\<dataContractSerializer>](datacontractserializer-element.md)
- [\<add>](add-of-declaredtypes-element.md)
