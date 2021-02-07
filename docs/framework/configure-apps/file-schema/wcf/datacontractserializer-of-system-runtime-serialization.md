---
description: 'Saiba mais sobre: <dataContractSerializer> de <System. Runtime. serialization>'
title: <dataContractSerializer> de <System. Runtime. Serialization>
ms.date: 03/30/2017
ms.assetid: d9b3d625-be3f-4768-8e0d-1b7e6929f6a8
ms.openlocfilehash: 3755005782ea773344326d211b9f8f115a97f2ae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754414"
---
# <a name="datacontractserializer-of-systemruntimeserialization"></a>\<dataContractSerializer> de \<system.runtime.serialization>

Contém dados de configuração para o <xref:System.Runtime.Serialization.DataContractSerializer> .  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.serialization>**](system-runtime-serialization.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<dataContractSerializer>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<configuration>
  <system.runtime.serialization>
    <dataContractSerializer ignoreExtensionDataObject="Boolean"
                            maxItemsInObjectGraph="Integer">
      <declaredTypes>
        <add type="String">
          <knownType type="String">
            <parameter index="Integer"
                       type="String" />
          </knownType>
        </add>
      </declaredTypes>
    <dataContractSerializer>
  </system.runtime.serialization>
</configuration>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|ignoreExtensionDataObject|Um valor booliano que especifica se é para ignorar os dados fornecidos pelo ponto de extremidade quando ele está sendo serializado ou desserializado. Esse atributo é configurável somente no `<dataContractSerializer>` `<behavior>` elemento abaixo.|  
|maxItemsInObjectGraph|Um inteiro que especifica o número máximo de itens a serem serializados ou desserializados. Esse atributo é 65536.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<declaredTypes>](declaredtypes.md)|Contém os tipos conhecidos que o <xref:System.Runtime.Serialization.DataContractSerializer> usa ao desserializar.<br /><br /> Para obter mais informações sobre contratos de dados e tipos conhecidos, consulte [tipos conhecidos de contrato de dados](../../../wcf/feature-details/data-contract-known-types.md).|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<system.runtime.serialization>](system-runtime-serialization.md)|Representa o elemento raiz da <xref:System.Runtime.Serialization> seção namespace e contém elementos para definir as opções do <xref:System.Runtime.Serialization.DataContractSerializer> .|  
  
## <a name="remarks"></a>Comentários  

 Para obter mais informações sobre tipos conhecidos, consulte <xref:System.Runtime.Serialization.DataContractSerializer> e [tipos conhecidos de contrato de dados](../../../wcf/feature-details/data-contract-known-types.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>
- [Tipos de contratos de dados conhecidos](../../../wcf/feature-details/data-contract-known-types.md)
