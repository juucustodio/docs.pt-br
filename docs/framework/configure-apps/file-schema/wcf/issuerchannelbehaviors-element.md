---
description: 'Saiba mais sobre: <issuerChannelBehaviors> elemento'
title: Elemento <issuerChannelBehaviors>
ms.date: 03/30/2017
ms.assetid: f7378673-8e9b-45b2-98d1-cf5dccdd8c40
no-loc:
- <system.serviceModel>
- <behaviors>
- <endpointBehaviors>
- <behavior>
- <clientCredentials>
- <issuedToken>
- <issuerChannelBehaviors>
- <dataContractSerializer>
ms.openlocfilehash: 6be79f2ee6afb442a7a399ce49df4ad59dff2db5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99725539"
---
# <a name="issuerchannelbehaviors-element"></a>\::: no-Loc ( <issuerChannelBehaviors> ):: Element

Contém uma coleção de comportamentos de ponto de extremidade de cliente do Windows Communication Foundation (WCF) (definida na configuração) a ser usada na comunicação com os serviços de token de serviço especificados. Os comportamentos definidos não podem incluir nenhum dos elementos [ \: :: no-Loc ( <clientCredentials> ):::](clientcredentials.md) .

[\<configuration>](../configuration-element.md)\
&nbsp;&nbsp;[\::: no-Loc (<> System. serviceModel):::](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[\::: no-Loc ( <behaviors> ):::](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\::: no-Loc ( <endpointBehaviors> ):::](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\::: no-Loc ( <behavior> ):::](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\::: no-Loc ( <clientCredentials> ):::](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[\::: no-Loc ( <issuedToken> ):::](issuedtoken.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\::: no-Loc ( <issuerChannelBehaviors> ):::

## <a name="syntax"></a>Syntax

```xml
<issuerChannelBehaviors>
  <add behaviorConfiguration="string"
       issuerAddress="string" />
</issuerChannelBehaviors>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

Nenhum.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[\<add>](add-of-issuerchannelbehaviors.md)|Adiciona um comportamento à coleção.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[\::: no-Loc ( <issuedToken> ):::](issuedtoken.md)|Especifica um token personalizado usado para autenticar um cliente para um serviço.|

## <a name="remarks"></a>Comentários

Use este elemento quando quaisquer comportamentos (que não sejam os comportamentos que incluem `<clientCredentials>` elementos) devem ser usados para se comunicar com um serviço. Por exemplo, se um elemento [ \: :: no-Loc ( <dataContractSerializer> ):::](datacontractserializer-element.md) Behavior deve ser incluído.

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
