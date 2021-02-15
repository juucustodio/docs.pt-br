---
description: 'Saiba mais sobre: <dispatcherSynchronization>'
title: <dispatcherSynchronization>
ms.date: 03/30/2017
ms.assetid: cc030f9c-4e38-4b14-94dc-9a0e41ec8e2d
ms.openlocfilehash: 93664dec3648ed58df7e3e5c0760f1694c60ba7e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99749594"
---
# \<dispatcherSynchronization>
  
Especifica um comportamento de ponto de extremidade que permite que um serviço envie respostas de forma assíncrona.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<dispatcherSynchronization>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<dispatcherSynchronizationBehavior asynchronousSendEnabled="Boolean"
                                   maxPendingReceives="Integer" />
```  
  
## <a name="type"></a>Tipo  
  
`Type`  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
  
As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos

| Atributo               | Descrição       |
| ----------------------- | ----------------- |
| asynchronousSendEnabled | Um booliano que especifica se o comportamento de envio assíncrono está habilitado. |
| `maxPendingReceives`    | Um inteiro que especifica o número de recebimentos simultâneos que podem ser emitidos no canal.<br /><br /> Esse valor deve ser configurado somente depois que você tiver configurado corretamente o comportamento de limitação de serviço. |

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

| Elemento | Descrição |  
| ------- | ----------- |  
| [\<behavior>](behavior-of-endpointbehaviors.md)|Especifica um comportamento de ponto de extremidade. |

## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Configuration.DispatcherSynchronizationElement>
- <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior>
