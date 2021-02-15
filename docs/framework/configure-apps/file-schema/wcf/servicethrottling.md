---
description: 'Saiba mais sobre: <serviceThrottling>'
title: <serviceThrottling>
ms.date: 03/30/2017
ms.assetid: a337d064-1e64-4209-b4a9-db7fdb7e3eaf
ms.openlocfilehash: eb65f6d60a266a367789d87e4e6ea10ebfd2c7a7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786675"
---
# \<serviceThrottling>

Especifica o mecanismo de limitação de um serviço do Windows Communication Foundation (WCF).  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceThrottling>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<serviceThrottling maxConcurrentCalls="Integer"
                   maxConcurrentInstances="Integer"
                   maxConcurrentSessions="Integer" />
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|maxConcurrentCalls|Um número inteiro positivo que limita o número de mensagens que são processadas atualmente por meio de um <xref:System.ServiceModel.ServiceHost>. As chamadas além do limite são enfileiradas. Definir esse valor como 0 é equivalente a defini-lo como Int32.MaxValue. O padrão é 16 * contagem de processador.|  
|maxConcurrentInstances|Um número inteiro positivo que limita o número de objetos <xref:System.ServiceModel.InstanceContext> executados ao mesmo tempo em um <xref:System.ServiceModel.ServiceHost>. As solicitações para criar instâncias adicionais serão enfileiradas e concluídas quando um slot abaixo do limite ficar disponível. A opção é a soma de maxConcurrentSessions e MaxConcurrentCalls|  
|maxConcurrentSessions|Um número inteiro positivo que limita o número de sessões que um objeto <xref:System.ServiceModel.ServiceHost> pode aceitar.<br /><br /> O serviço aceitará conexões além do limite, mas somente os canais abaixo do limite estarão ativos (as mensagens são lidas do canal). Definir esse valor como 0 é equivalente a defini-lo como Int32.MaxValue. O padrão é 100 * contagem de processadores.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|Especifica um elemento de comportamento.|  
  
## <a name="remarks"></a>Comentários  

 Os controles de limitação colocam limites no número de chamadas simultâneas, instâncias ou sessões para evitar a sobrecarga de consumo de recursos.  
  
 Um rastreamento é gravado cada vez que o valor dos atributos é atingido. O primeiro rastreamento é gravado como um aviso.  
  
## <a name="example"></a>Exemplo  

 O seguinte exemplo de configuração especifica que o serviço limita o máximo de chamadas simultâneas para 2, e o número máximo de instâncias simultâneas para 10. Para obter um exemplo detalhado de como executar este exemplo, consulte [limitação](../../../wcf/samples/throttling.md).  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
      <serviceDebug includeExceptionDetailInFaults="False" />
      <serviceMetadata httpGetEnabled="True" />
      <!-- Specify throttling behavior -->
      <serviceThrottling maxConcurrentCalls="2"
                         maxConcurrentInstances="10" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
- <xref:System.ServiceModel.Configuration.ServiceThrottlingElement>
- [Utilizando o ServiceThrottlingBehavior para controlar o desempenho de serviço do WCF](../../../wcf/feature-details/using-servicethrottlingbehavior-to-control-wcf-service-performance.md)
