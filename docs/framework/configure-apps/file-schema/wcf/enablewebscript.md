---
description: 'Saiba mais sobre: <enableWebScript>'
title: <enableWebScript>
ms.date: 03/30/2017
ms.assetid: 9c7e96e1-af70-4e6e-ac5c-d67929dddbaa
ms.openlocfilehash: f357bf1ab726cd434a16b2daa9c8115afe7d4430
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99725877"
---
# \<enableWebScript>

Esse elemento habilita o comportamento do ponto de extremidade que torna possível consumir o serviço de páginas da Web do ASP.NET AJAX.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<enableWebScript>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<enableWebScript />
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|Especifica o conjunto de comportamentos de ponto de extremidade.|  
  
## <a name="remarks"></a>Comentários  

 Esse comportamento só deve ser usado em conjunto com a [\<webHttpBinding>](webhttpbinding.md) associação padrão ou com o [\<webMessageEncoding>](webmessageencoding.md) elemento de associação.  Para obter mais informações sobre esse comportamento, consulte <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> .  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.WebScriptEnablingElement>
- <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>
- [Integração de AJAX e suporte para JSON](../../../wcf/feature-details/ajax-integration-and-json-support.md)
- [\<webHttp>](webhttp.md)
