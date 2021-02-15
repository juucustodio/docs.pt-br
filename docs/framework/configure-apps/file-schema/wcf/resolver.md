---
description: 'Saiba mais sobre: <resolver>'
title: <resolver>
ms.date: 03/30/2017
ms.assetid: 0c00200c-f135-4e5c-a024-76b72bcbc021
ms.openlocfilehash: 338f9342d1ef14f3d96dada17fb9f6d893c86bee
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99683353"
---
# \<resolver>

Especifica um resolvedor de pares que é usado para resolver uma ID de malha de mesmo nível para um conjunto de endereços de nó par que representa vários nós que participam da malha.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<netPeerTcpBinding>**](netpeertcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<resolver>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<resolver mode="Auto/Custom/Pnrp"
          referralPolicy="DoNotShare/Service/Share">
</resolver>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`mode`|Uma cadeia de caracteres que especifica se a instância do resolvedor de pares associada a esse serviço é específica do PNRP, um resolvedor personalizado ou determinado automaticamente. Esse atributo é do tipo <xref:System.ServiceModel.PeerResolvers.PeerResolverMode> .|  
|`referralPolicy`|Uma cadeia de caracteres que especifica a maneira como as referências são compartilhadas entre os pares. Esse atributo é do tipo <xref:System.ServiceModel.PeerResolvers.PeerReferralPolicy> .|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<headers>](headers.md)|Especifica as configurações para um serviço resolvedor de pares personalizado.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<binding>](bindings.md)|Define todos os recursos de associação do [\<netPeerTcpBinding>](netpeertcpbinding.md) .|  
  
## <a name="remarks"></a>Comentários  

 Um resolvedor de nome de par é um serviço de descoberta usado por canais de mesmo nível para localizar nós de mesmo nível que participam de uma malha de mesmo nível. Ele também é usado para "registrar" um nó com uma malha de mesmo nível, o mecanismo pelo qual o nó par se torna conhecido e disponível na malha de pares. Para obter mais informações sobre resolvedores de pares, consulte [resolvedores de pares](../../../wcf/feature-details/peer-resolvers.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.PeerResolver>
- <xref:System.ServiceModel.PeerResolvers.PeerResolverSettings>
- <xref:System.ServiceModel.NetPeerTcpBinding.Resolver%2A>
- <xref:System.ServiceModel.Configuration.NetPeerTcpBindingElement.Resolver%2A>
- <xref:System.ServiceModel.Configuration.PeerResolverElement>
- [Resolvedor peer](../../../wcf/feature-details/peer-resolvers.md)
- [Adicionando um resolvedor personalizado a um aplicativo PeerChannel](/previous-versions/ms730105(v=vs.90))
