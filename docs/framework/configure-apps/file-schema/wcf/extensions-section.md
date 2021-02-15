---
description: 'Saiba mais sobre: <extensions> seção'
title: <extensions> Section
ms.date: 03/30/2017
ms.assetid: 53a59fb6-dede-47ec-9384-b3c2e8f0c1fa
ms.openlocfilehash: 65b1de76155b1e3fbd8e5f14a5f4a1cb8c180ec1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99664685"
---
# <a name="extensions-section"></a>\<extensions> Section

Esta seção de configuração contém uma coleção de extensões, que permitem ao usuário criar associações definidas pelo usuário, comportamentos e outros aspectos de extensões.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<extensions>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.serviceModel>
  <extensions>
    <bindingExtensions>
    </bindingExtensions>
    <behaviorExtensions>
    </behaviorExtensions>
    <bindingElementExtensions>
    </bindingElementExtensions>
    <endpointExtensions>
    </endpointExtensions>
  </extensions>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<behaviorExtensions>](behaviorextensions.md)|Esta seção contém elementos filho que especificam extensões de comportamento, que permitem ao usuário personalizar comportamentos de serviço ou ponto de extremidade.|  
|[\<bindingElementExtensions>](bindingelementextensions.md)|Esta seção habilita o uso de um elemento de associação personalizado de um computador ou arquivo de configuração de aplicativo.|  
|[\<bindingExtensions>](bindingextensions.md)|Esta seção contém elementos filho que especificam extensões de associação, que permitem ao usuário personalizar associações.|  
|[\<endpointExtensions>](endpointextensions.md)|Esta seção contém elementos filho que registram pontos de extremidade padrão.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|sistema.ServiceModel|O elemento raiz de todos os elementos de configuração do WCF.|
