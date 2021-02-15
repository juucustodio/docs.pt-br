---
description: 'Saiba mais sobre: como configurar o acompanhamento com o WorkflowServiceHost'
title: 'Como: configurar o acompanhamento com WorkflowServiceHost'
ms.date: 03/30/2017
ms.assetid: ed1485fe-7529-4351-bca3-8bb915260b17
ms.openlocfilehash: 11c48c3989ab9b788c1e6834d8cbfe53e2b8a53e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734822"
---
# <a name="how-to-configure-tracking-with-workflowservicehost"></a>Como: configurar o acompanhamento com WorkflowServiceHost

Este tópico explica como configurar o acompanhamento de um [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] fluxo de trabalho hospedado no <xref:System.ServiceModel.Activities.WorkflowServiceHost> . Ele é configurado por meio de um arquivo de Web.config especificando um comportamento de serviço.  
  
### <a name="configure-tracking-in-configuration"></a>Configurar o controle na configuração  
  
1. Adicione o <xref:System.Activities.Tracking.EtwTrackingParticipant> usando o `behavior` elemento <> em um arquivo de configuração, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <behaviors>  
       <serviceBehaviors>  
         <behavior>  
           <etwTracking profileName="Sample Tracking Profile" />  
         </behavior>
       </serviceBehaviors>  
    </behaviors>  
    ```  
  
    > [!NOTE]
    > O exemplo de configuração anterior está usando uma configuração simplificada. Para obter mais informações, consulte [configuração simplificada](../simplified-configuration.md).  
  
     O exemplo de configuração anterior adiciona um <xref:System.Activities.Tracking.EtwTrackingParticipant> e especifica um nome de perfil de controle. Os perfis de rastreamento são criados em um `trackingProfile` elemento <> dentro de um `tracking` elemento> <. O perfil de controle contém consultas de acompanhamento que permitem que um participante de controle assine eventos de fluxo de trabalho emitidos quando o estado de uma instância de fluxo de trabalho é alterado no tempo de execução. O exemplo a seguir mostra como criar um perfil de controle.  
  
    ```xml  
    <system.serviceModel>  
        <tracking>
         <trackingProfile name="Sample Tracking Profile">  
            <workflow activityDefinitionId="*">  
               <workflowInstanceQueries>  
                 <workflowInstanceQuery>  
                    <states>  
                       <state name="Started"/>  
                       <state name="Completed"/>  
                    </states>  
                </workflowInstanceQuery>  
             </workflowInstanceQueries>  
           </workflow>  
         </trackingProfile>
       </tracking>  
    </system.serviceModel>  
    ```  
  
     Para obter mais informações sobre perfis de rastreamento, consulte [perfis de rastreamento](../../windows-workflow-foundation/tracking-profiles.md).  
  
     Para obter mais informações sobre o rastreamento em geral, consulte rastreamento [e acompanhamento de fluxo de trabalho](../../windows-workflow-foundation/workflow-tracking-and-tracing.md).  
  
### <a name="configure-tracking-in-code"></a>Configurar o acompanhamento no código  
  
1. Adicione o <xref:System.Activities.Tracking.EtwTrackingParticipant> usando o <xref:System.ServiceModel.Activities.Description.EtwTrackingBehavior> comportamento no código, conforme mostrado no exemplo a seguir.  
  
    ```csharp  
    host.Description.Behaviors.Add(new EtwTrackingBehavior { ProfileName = "Sample Tracking Profile" });  
    ```  
  
     O exemplo de código anterior adiciona um <xref:System.Activities.Tracking.EtwTrackingParticipant> e especifica um nome de perfil de controle. Os perfis de rastreamento são criados em um `trackingProfile` elemento <> dentro de um `tracking` elemento <>, conforme mostrado na seção anterior.  
  
     Para obter mais informações sobre perfis de rastreamento, consulte [perfis de rastreamento](../../windows-workflow-foundation/tracking-profiles.md).  
  
     Para obter mais informações sobre o rastreamento em geral, consulte rastreamento [e acompanhamento de fluxo de trabalho](../../windows-workflow-foundation/workflow-tracking-and-tracing.md). Para obter um exemplo de como configurar o acompanhamento programaticamente, consulte [Configurando o acompanhamento de um fluxo](../../windows-workflow-foundation/configuring-tracking-for-a-workflow.md)  
  
## <a name="see-also"></a>Consulte também

- [Configuração simplificada para serviços do WCF](../samples/simplified-configuration-for-wcf-services.md)
- [Serviços de fluxo de trabalho](workflow-services.md)
- [Controlando perfis](../../windows-workflow-foundation/tracking-profiles.md)
