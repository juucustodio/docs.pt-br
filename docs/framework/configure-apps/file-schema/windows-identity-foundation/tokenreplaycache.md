---
description: 'Saiba mais sobre: <tokenReplayCache>'
title: <tokenReplayCache>
ms.date: 03/30/2017
ms.assetid: 1572ab23-6933-41b5-bfb4-0c4548145500
author: BrucePerlerMS
ms.openlocfilehash: 793b1f88a9eeb0ebce4cd440e248e81377f17e9b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99748993"
---
# \<tokenReplayCache>

Registra um cache de reprodução de token com um serviço ou uma coleção de manipulador de token de segurança.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<caches>**](caches.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<tokenReplayCache>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <caches>  
      <tokenReplayCache type=xs:string>  
      </tokenReplayCache>  
    </caches>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|type|Um tipo que deriva da <xref:System.IdentityModel.Tokens.TokenReplayCache> classe. Para obter mais informações sobre como especificar um personalizado `type` , consulte [referências de tipo personalizado].
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<caches>](caches.md)|Registra os caches usados por um serviço ou uma coleção de manipulador de token de segurança.|  
  
## <a name="remarks"></a>Comentários  

 O cache de reprodução de token é usado para detectar tokens reproduzidos. A detecção de reprodução de token é habilitada pelo [\<tokenReplayDetection>](tokenreplaydetection.md) elemento, que também especifica o tempo de expiração máximo para tokens.  
  
## <a name="example"></a>Exemplo  

 O XML a seguir mostra a configuração de um cache personalizado para detectar tokens reproduzidos.  
  
```xml  
<caches>  
  <tokenReplayCache type="MyCacheLibrary.MyTokenReplayCache, MyCacheLibrary">  
  </tokenReplayCache>  
</caches>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.IdentityModel.Tokens.TokenReplayCache>
- [\<tokenReplayDetection>](tokenreplaydetection.md)
