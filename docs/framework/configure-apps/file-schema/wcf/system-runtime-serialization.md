---
description: 'Saiba mais sobre: <System. Runtime. Serialization>'
title: <system.runtime.serialization>
ms.date: 03/30/2017
ms.assetid: a8cebf4c-06d2-4667-8f5b-c3e1fc90df6f
ms.openlocfilehash: cf1d95c8650e4b6979d4f34b0bed1fa395911f2d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786623"
---
# \<system.runtime.serialization>

Representa o elemento raiz da <xref:System.Runtime.Serialization> seção namespace e contém elementos para definir as opções do <xref:System.Runtime.Serialization.DataContractSerializer> .  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;**\<system.runtime.serialization>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<configuration>
  <system.runtime.serialization>
    <dataContractSerializer ignoreExtensionDataObject="Boolean"
                            maxItemsInObjectGraph="Integer">
      <declaredTypes>
        <add type="String">
          <knownType type="String">
            <parameter index="Integer" />
          </knownType>
        </add>
      </declaredTypes>
    <dataContractSerializer>
  </system.runtime.serialization>
</configuration>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<dataContractSerializer>](datacontractserializer-of-system-runtime-serialization.md)|Permite que a adição de tipos conhecidos seja usada na desserialização.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<configuration> Elementos](../configuration-element.md)|O elemento de nível superior para configuração.|  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization>
- [Usando contratos de dados](../../../wcf/feature-details/using-data-contracts.md)
- [Tipos de contratos de dados conhecidos](../../../wcf/feature-details/data-contract-known-types.md)
