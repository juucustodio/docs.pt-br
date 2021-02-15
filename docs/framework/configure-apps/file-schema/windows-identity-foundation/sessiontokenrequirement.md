---
description: 'Saiba mais sobre: <sessionTokenRequirement>'
title: <sessionTokenRequirement>
ms.date: 03/30/2017
ms.assetid: 496a1735-cbb7-49d5-a6aa-dd5550462073
author: BrucePerlerMS
ms.openlocfilehash: 8f2868df4939dc0dc7c779eb9ca5a35a6b996fc6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99698265"
---
# \<sessionTokenRequirement>

Fornece a configuração para a <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> classe ou classes derivadas.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<sessionTokenRequirement>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel">  
        <sessionTokenRequirement lifetime=TimeSpan >  
        </sessionTokenRequirement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|lifetime|Especifica o tempo de vida dos tokens de sessão.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<add>](add.md)|Adiciona o manipulador de token de segurança especificado à coleção de manipulador de token.|  
  
## <a name="example"></a>Exemplo  
  
```xml  
<add type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel">
    <sessionTokenRequirement lifetime="10:00" />  
</add>  
```
