---
description: 'Saiba mais sobre: <claimsAuthenticationManager>'
title: <claimsAuthenticationManager>
ms.date: 03/30/2017
ms.assetid: 6d30a450-6d13-4671-81a8-77e0204500c5
author: BrucePerlerMS
ms.openlocfilehash: 5a94861d6b2684b9f66c7d5e14f72aa419a0c66f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99664243"
---
# \<claimsAuthenticationManager>

Registra um Gerenciador de autenticação de declarações para as declarações de entrada.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<claimsAuthenticationManager>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthenticationManager type=xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthenticationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|type|Especifica um tipo personalizado que deriva da <xref:System.Security.Claims.ClaimsAuthenticationManager> classe. Para obter mais informações sobre como especificar o `type` atributo, consulte [referências de tipo personalizado].|  
  
### <a name="child-elements"></a>Elementos filho  

 Se não houver nenhum `type` atributo ou se o `type` atributo fizer referência à <xref:System.Security.Claims.ClaimsAuthenticationManager> classe, o `<claimsAuthenticationManager>` elemento não assumirá elementos filho; no entanto, as classes derivadas de <xref:System.Security.Claims.ClaimsAuthenticationManager> podem definir elementos de configuração filho.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|Especifica as configurações de identidade de nível de serviço.|  
  
## <a name="remarks"></a>Comentários  

 O comportamento padrão fornecido por meio da <xref:System.Security.Claims.ClaimsAuthenticationManager> classe ecoa as declarações de entrada. Se nenhum `type` atributo for especificado ou se o `type` atributo especificar a <xref:System.Security.Claims.ClaimsAuthenticationManager> classe, o `<claimsAuthenticationManager>` elemento não assumirá elementos filho. Você pode especificar o `type` atributo para registrar um tipo derivado da <xref:System.Security.Claims.ClaimsAuthenticationManager> classe para implementar o comportamento personalizado. Classes derivadas podem dar suporte à configuração por meio de elementos filho do `<claimsAuthenticationManager>` elemento, substituindo o <xref:System.Security.Claims.ClaimsAuthenticationManager.LoadCustomConfiguration%2A> método para lidar com esses elementos. O esquema definido para os elementos filho é até o designer da classe.  
  
 O `<claimsAuthenticationManager>` elemento define a <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthenticationManager%2A?displayProperty=nameWithType> propriedade.  
  
## <a name="example"></a>Exemplo  
  
```xml  
<system.identityModel>  
    <identityConfiguration name="MyIdentity">  
      <claimsAuthenticationManager type="MyNamespace.CustomClaimsAuthenticationManager, MyAssembly"/>
    </identityConfiguration>  
</system.identityModel>  
```
