---
description: 'Saiba mais sobre: usando o ServiceThrottlingBehavior para controlar o desempenho do serviço WCF'
title: Utilizando o ServiceThrottlingBehavior para controlar o desempenho de serviço do WCF
ms.date: 03/30/2017
helpviewer_keywords:
- behavior [WCF], service performance
ms.assetid: f9dc120c-dc24-49d5-930e-b22f5bc73423
ms.openlocfilehash: 4a53c89c6b17402b7dd32120d049426052e4f9e0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704414"
---
# <a name="using-servicethrottlingbehavior-to-control-wcf-service-performance"></a>Utilizando o ServiceThrottlingBehavior para controlar o desempenho de serviço do WCF

A <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> classe expõe as propriedades que você pode usar para limitar quantas instâncias ou sessões são criadas no nível do aplicativo. Usando esse comportamento, você pode ajustar o desempenho do seu aplicativo Windows Communication Foundation (WCF).  
  
## <a name="controlling-service-instances-and-concurrent-calls"></a>Controlando instâncias de serviço e chamadas simultâneas  

 Use a <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> propriedade para especificar o número máximo de mensagens processando ativamente em uma <xref:System.ServiceModel.ServiceHost> classe e a <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> propriedade para especificar o número máximo de <xref:System.ServiceModel.InstanceContext> objetos no serviço.  
  
 Como determinar as configurações para essas propriedades geralmente ocorre após a experiência do mundo real em executar o aplicativo em relação às cargas, as configurações das <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> Propriedades normalmente são especificadas em um arquivo de configuração de aplicativo usando o [\<serviceThrottling>](../../configure-apps/file-schema/wcf/servicethrottling.md) elemento.  
  
 O exemplo de código a seguir mostra o uso da <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> classe de um arquivo de configuração de aplicativo que define as <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A> <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> Propriedades, e como <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> 1 como um exemplo trivial. A experiência do mundo real determina as configurações ideais para qualquer aplicativo específico.  
  
 [!code-xml[ServiceThrottlingBehavior#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/servicethrottlingbehavior/cs/hostapplication.exe.config#3)]  
  
 O comportamento exato do tempo de execução depende dos valores das <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> Propriedades e <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> , que controlam quantas mensagens podem ser executadas dentro de uma operação de uma vez e os tempos de vida do serviço <xref:System.ServiceModel.InstanceContext> relativos às sessões de canal de entrada, respectivamente.  
  
 Para obter detalhes, consulte <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> e <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> .  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
- <xref:System.ServiceModel.NetTcpBinding.MaxConnections%2A>
