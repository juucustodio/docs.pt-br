---
description: 'Saiba mais sobre: <behaviors> do fluxo de trabalho'
title: <behaviors> do fluxo de trabalho
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 3c6017b6-0c4f-4192-bd67-9515f5d1ec82
ms.openlocfilehash: 5154a389aded34065cc7bdb11d1c73d71ca9f9f5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99698187"
---
# <a name="behaviors-of-workflow"></a>\<behaviors> do fluxo de trabalho

Esse elemento contém a coleção de **Imcomportamentos** .  Cada elemento na coleção define elementos de comportamento consumidos pelos serviços de fluxo de trabalho. Cada elemento de comportamento é identificado por seu atributo de **nome** exclusivo.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<behaviors>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<serviceBehaviors>](servicebehaviors-of-workflow.md)|Esta seção de configuração representa todos os comportamentos definidos para um serviço de fluxo de trabalho específico.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<system.serviceModel>](../wcf/system-servicemodel.md)|O elemento raiz de todos os elementos de configuração do fluxo de trabalho.|  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.BehaviorsSection>
- <xref:System.ServiceModel.Configuration.ServiceBehaviorElementCollection>
- <xref:System.ServiceModel.Configuration.ServiceBehaviorElement>
- [Configurando e estendendo o runtime com comportamentos](../../../wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)
