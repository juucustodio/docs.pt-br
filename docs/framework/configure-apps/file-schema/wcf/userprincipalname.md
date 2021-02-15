---
description: 'Saiba mais sobre: <userPrincipalName>'
title: <userPrincipalName>
ms.date: 03/30/2017
ms.assetid: 68032f69-149e-4613-bae4-18314d4fd294
ms.openlocfilehash: 73ace3d6f3d5cb88f2630a4a2ae319decf420021
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99664412"
---
# \<userPrincipalName>

Especifica o nome principal do usuário (UPN) de um serviço a ser autenticado pelo cliente.  
  
Para obter mais informações sobre como definir o UPN, consulte [identidade de serviço e autenticação](../../../wcf/feature-details/service-identity-and-authentication.md).  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpoint>**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<identity>**](identity.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<userPrincipalName>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<userPrincipalName value="String" />
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|value|Um nome de conta de usuário (às vezes chamado de nome de logon do usuário) e um nome de domínio que identifica o domínio no qual a conta de usuário está localizada. Esse é o uso padrão para fazer logon em um domínio do Windows. O formato é: someone@example.com (como para um endereço de email).|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<identity>](identity.md)|Especifica a identidade do serviço a ser autenticado pelo cliente.|  
  
## <a name="remarks"></a>Comentários  

 Um cliente de Windows Communication Foundation seguro (WCF) que se conecta a um ponto de extremidade com essa identidade usa o UPN ao executar a autenticação SSPI com o ponto de extremidade.  
  
## <a name="example"></a>Exemplo  

 O código de configuração a seguir especifica o UPN do serviço a ser autenticado pelo cliente.  
  
```xml  
<identity>
  <userPrincipalName value="someone@cohowinery.com" />
</identity>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- <xref:System.ServiceModel.UpnEndpointIdentity>
- [Identidade e autenticação de serviço](../../../wcf/feature-details/service-identity-and-authentication.md)
- [\<identity>](identity.md)
