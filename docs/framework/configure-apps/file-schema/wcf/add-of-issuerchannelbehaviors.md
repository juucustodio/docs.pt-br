---
description: 'Saiba mais sobre: <add> de <issuerChannelBehaviors>'
title: <add> de <issuerChannelBehaviors>
ms.date: 03/30/2017
ms.assetid: 50710506-e28f-45dd-ab7e-bff6f44173db
ms.openlocfilehash: ccd8ba015b7a6837c74ce2c051a794d36ce8ceaa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99750293"
---
# <a name="add-of-issuerchannelbehaviors"></a>\<add> de \<issuerChannelBehaviors>

Adiciona um comportamento de ponto de extremidade a ser usado ao se comunicar com um STS.

> [!NOTE]
> Se qualquer comportamento de ponto de extremidade contiver um [\<clientCredentials>](clientcredentials.md) elemento, uma exceção será lançada.

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedToken>**](issuedtoken.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuerChannelBehaviors>**](issuerchannelbehaviors-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  

## <a name="syntax"></a>Syntax

```xml
<add issuerAddress="string"
     behaviorConfiguration="string" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|issuerAddress|O URI do emissor do token de segurança com o qual se comunicar.|
|behaviorConfiguration|O nome de um comportamento de ponto de extremidade definido no mesmo arquivo de configuração.|

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[\<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)|Contém uma coleção de comportamentos de ponto de extremidade de cliente do Windows Communication Foundation (WCF) a ser usada ao se comunicar com os serviços de token de serviço especificados.|

## <a name="remarks"></a>Comentários

`issuerAddress` contém o URI do serviço de token de segurança com o qual o cliente deseja se comunicar. `behaviorConfiguration` aponta para um comportamento de ponto de extremidade que o aplicativo usa nos canais criados por Windows Communication Foundation (WCF) para obter os tokens emitidos dos serviços de token de segurança.

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.IssuerChannelBehaviors%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElement>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElementCollection>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential.IssuerChannelBehaviors%2A>
- [Identidade e autenticação de serviço](../../../wcf/feature-details/service-identity-and-authentication.md)
- [Comportamentos de segurança](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Federação e tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Protegendo serviços e clientes](../../../wcf/feature-details/securing-services-and-clients.md)
- [Protegendo clientes](../../../wcf/securing-clients.md)
- [Como: criar um cliente federado](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [Como: configurar um emissor local](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [Federação e tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [\<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)
