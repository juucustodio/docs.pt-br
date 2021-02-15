---
description: 'Saiba mais sobre: <defaultPorts>'
title: <defaultPorts>
ms.date: 03/30/2017
ms.assetid: 725d4ee5-bd46-4f0e-9c20-30ba75d6eb2c
ms.openlocfilehash: 7cd0635568bf80734900f5e54f918150ea657322
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803900"
---
# \<defaultPorts>

Uma coleção de portas padrão que listam os pontos de extremidade de comunicação padrão que o aplicativo cliente ouve.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<useRequestHeadersForMetadataAddress>**](userequestheadersformetadataaddress.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<defaultPorts>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<useRequestHeadersForMetadataAddress>
  <defaultPorts>
    <add scheme="http"
         port="integer" />
  </defaultPorts>
</useRequestHeadersForMetadataAddress>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<add> desse \<defaultPorts>](add-of-defaultports.md)|Um ponto de extremidade de comunicação padrão que o aplicativo cliente ouve.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<useRequestHeadersForMetadataAddress>](userequestheadersformetadataaddress.md)|Uma lista de portas padrão.|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Configuration.DefaultPortElementCollection>
