---
description: 'Saiba mais sobre: <issuer> de <issuedTokenParameters>'
title: <issuer> de <issuedTokenParameters>
ms.date: 03/30/2017
ms.assetid: d6a95f32-d58c-40fc-8658-dd92564d3c90
ms.openlocfilehash: 7d67583eda22414750631b6dff40f6e6ea8831e4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99725643"
---
# <a name="issuer-of-issuedtokenparameters"></a>\<issuer> de \<issuedTokenParameters>

Especifica o serviço de token de segurança (STS) que emite tokens de segurança.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedTokenParameters>**](issuedtokenparameters.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<issuer>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<issuer address="Uri" />
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|address|Cadeia de caracteres obrigatória. A URL do STS.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<headers>](headers-element.md)|Uma coleção de cabeçalhos de endereço para os pontos de extremidade que o construtor pode criar.|  
|[\<identity>](identity.md)|Ao usar um token emitido, especifica as configurações que permitem que o cliente autentique o servidor.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<issuedTokenParameters>](issuedtokenparameters.md)|Especifica o token emitido atual.|  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.AdditionalRequestParameters%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement.AdditionalRequestParameters%2A>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Identidade e autenticação de serviço](../../../wcf/feature-details/service-identity-and-authentication.md)
- [Federação e tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Recursos de segurança com associações personalizadas](../../../wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [Federação e tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Associações](../../../wcf/bindings.md)
- [Estendendo associações](../../../wcf/extending/extending-bindings.md)
- [Associações personalizadas](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [Como: criar uma associação personalizada utilizando o SecurityBindingElement](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [Segurança de associação personalizada](../../../wcf/samples/custom-binding-security.md)
