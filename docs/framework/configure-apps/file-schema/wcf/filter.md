---
description: 'Saiba mais sobre: <filter>'
title: <filter>
ms.date: 03/30/2017
ms.assetid: 3266700b-904b-44e4-93a7-e06a1a445100
ms.openlocfilehash: 993d2265ac3a714475e8cbe9e8a2c3f93c46bde2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99664672"
---
# \<filter>

Define um filtro de roteamento, que determina o tipo de Windows Communication Foundation (WCF) <xref:System.ServiceModel.Dispatcher.MessageFilter> a ser usado ao avaliar mensagens recebidas, bem como quaisquer dados de suporte ou parâmetros exigidos pelo filtro.

[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;[**\<routing>**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<filters>**](filters-of-routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<filter>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<routing>
  <filters>
    <filter customType="String"
            filterData="String"
            filterType="Action/Address/AddressPrefix/And/Custom/Endpoint/MatchAll/XPath"
            name="String" />
  </filters>
</routing>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

| Atributo  | Descrição |
| ---------- | ----------- |
| CustomType | Uma cadeia de caracteres que contém o nome do tipo totalmente qualificado do tipo personalizado a ser usado como um filtro. Se `filterType` é definido como `custom` , esse atributo contém o nome de tipo totalmente qualificado da classe a ser criada.  `filterData` também pode conter valores a serem usados durante a avaliação do filtro de tipo personalizado. |
| filterData | Uma cadeia de caracteres que contém os dados de filtro. Para obter mais informações sobre como especificar esse atributo, consulte <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A> . |
| filterType | Uma cadeia de caracteres que contém o tipo de filtro. Esse atributo é do <xref:System.ServiceModel.Routing.Configuration.FilterType> tipo.  Para obter mais informações sobre como isso funciona com o `filterData` atributo, consulte <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A> . |
| name       | Uma cadeia de caracteres que contém o nome exclusivo deste elemento de filtro. |

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

| Elemento | Descrição |
| ------- | ----------- |
| [\<routing>](routing.md) | Uma seção de configuração para definir um conjunto de filtros de roteamento, que determinam o tipo de Windows Communication Foundation (WCF) <xref:System.ServiceModel.Dispatcher.MessageFilter> a ser usado ao avaliar mensagens de entrada. |

## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Routing.Configuration.FilterElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A?displayProperty=nameWithType>
- <xref:System.ServiceModel.Routing.Configuration.FilterType?displayProperty=nameWithType>
