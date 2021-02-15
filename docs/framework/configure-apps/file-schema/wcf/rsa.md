---
description: 'Saiba mais sobre: <rsa>'
title: <rsa>
ms.date: 03/30/2017
ms.assetid: ae1f2267-e40d-42ff-8abf-06ab7067bdb9
ms.openlocfilehash: 5e558e608ec1196081166d01415e12fb2c3083b0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786870"
---
# \<rsa>

Um cliente WCF seguro que se conecta a um ponto de extremidade com essa identidade verifica se as declarações apresentadas pelo servidor contêm uma declaração que contém a chave pública RSA usada para construir essa identidade.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpoint>**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<identity>**](identity.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<rsa>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<rsa value="String" />
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|value|Cadeia de caracteres opcional. O valor da chave pública RSA a ser comparado no cliente.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<identity>](identity.md)|Especifica a identidade do serviço a ser autenticado pelo cliente.|  
  
## <a name="remarks"></a>Comentários  

 Uma verificação RSA permite restringir especificamente a autenticação a um único certificado com base em sua chave RSA ou gerar seu próprio valor de chave RSA. Isso permite a autenticação mais estrita de uma chave RSA específica na despesa do serviço que não está mais funcionando com os clientes existentes se o valor da chave RSA for alterado.  
  
 Para obter mais informações sobre como usar a identidade para validar um serviço para um cliente, consulte [identidade e autenticação de serviço](../../../wcf/feature-details/service-identity-and-authentication.md).  
  
## <a name="example"></a>Exemplo  

 O código de configuração a seguir especifica o valor de chave pública de um certificado X. 509 que é usado para autenticar um servidor.  
  
```xml  
<identity>
  <rsa value="0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000" />
</identity>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- <xref:System.ServiceModel.RsaEndpointIdentity>
- [Identidade e autenticação de serviço](../../../wcf/feature-details/service-identity-and-authentication.md)
- [\<identity>](identity.md)
