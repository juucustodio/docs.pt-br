---
description: 'Saiba mais sobre: visão geral dos serviços de fluxo de trabalho de hospedagem'
title: Visão geral de serviços de fluxo de trabalho de hospedagem
ms.date: 03/30/2017
ms.assetid: 19f3704f-06bf-4eeb-8724-5224e02d7ead
ms.openlocfilehash: e183dfd7428c11cf20e731ab4a9975a7388b6f98
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743077"
---
# <a name="hosting-workflow-services-overview"></a>Visão geral de serviços de fluxo de trabalho de hospedagem

Os serviços de fluxo de trabalho devem ser hospedados para execução. O <xref:System.ServiceModel.WorkflowServiceHost> é o host de fluxo de trabalho pronto para uso que dá suporte a várias instâncias, configurações e mensagens do WCF (embora os fluxos de trabalho não sejam obrigados a usar o sistema de mensagens para serem hospedados).  Ele também se integra com persistência, controle e controle de instância por meio de um conjunto de comportamentos de serviço.  Assim como o WCF <xref:System.ServiceModel.ServiceHost> , o <xref:System.ServiceModel.WorkflowServiceHost> pode ser hospedado internamente em qualquer aplicativo .net gerenciado ou hospedado na Web (como um arquivo. xamlx) no IIS/WAS.  Os tópicos nesta seção descrevem como hospedar um serviço de fluxo de trabalho.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Serviços de fluxo de trabalho de hospedagem](hosting-workflow-services.md)  
 Descreve os serviços de fluxo de trabalho de hospedagem.  
  
 [Internos do host de serviço de fluxo de trabalho](workflow-service-host-internals.md)  
 Descreve como o <xref:System.ServiceModel.WorkflowServiceHost> processa as mensagens de entrada.  
  
 [Extensibilidade de host de serviço do fluxo de trabalho](workflow-service-host-extensibility.md)  
 Descreve como estender a funcionalidade do host do serviço de fluxo de trabalho.  
  
 [Ponto de extremidade de controle de fluxo de trabalho](workflow-control-endpoint.md)  
 Descreve como definir um ponto de extremidade que permite criar instâncias de fluxo de trabalho.
  
 [Como: hospedar um serviço de fluxo de trabalho com o Windows Server App Fabric](how-to-host-a-workflow-service-with-windows-server-app-fabric.md)  
 Demonstra como hospedar um serviço de fluxo de trabalho existente no Windows Server app Fabric.  
  
 [Configurando WorkflowServiceHost](configuring-workflowservicehost.md)  
 Descreve como controlar persistência, controle, ociosidade e comportamento de exceção sem tratamento.  
  
## <a name="reference"></a>Referência  

 <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
 <xref:System.ServiceModel.Activities.WorkflowService>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactory>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactoryBase>  
  
 <xref:System.ServiceModel.Activation.WorkflowServiceHostFactory>  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Serviços de fluxo de trabalho](workflow-services.md)
