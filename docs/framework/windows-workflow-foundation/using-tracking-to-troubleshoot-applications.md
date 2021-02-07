---
description: 'Saiba mais sobre: usando o rastreamento para solucionar problemas de aplicativos'
title: Usando o controle para solucionar problemas de aplicativos
ms.date: 03/30/2017
ms.assetid: 8851adde-c3c2-4391-9523-d8eb831490af
ms.openlocfilehash: 9ff2c1b9a4a35a75a9f4d2229b5b43d6607e7557
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754986"
---
# <a name="using-tracking-to-troubleshoot-applications"></a>Usando o controle para solucionar problemas de aplicativos

Windows Workflow Foundation (WF) permite que você acompanhe informações relacionadas ao fluxo de trabalho para fornecer detalhes sobre a execução de um aplicativo ou serviço Windows Workflow Foundation. Windows Workflow Foundation hosts são capazes de capturar eventos de fluxo de trabalho durante a execução de uma instância de fluxo de trabalho. Se o fluxo de trabalho gerar falhas ou exceções, você poderá usar os detalhes de rastreamento de Windows Workflow Foundation para solucionar problemas de processamento.  
  
## <a name="troubleshooting-a-wf-using-wf-tracking"></a>Solução de problemas um WF usando o rastreamento de WF  

 Para detectar falhas no processamento de uma atividade de Windows Workflow Foundation, você pode habilitar o acompanhamento com um perfil de controle que consulta um <xref:System.Activities.Tracking.ActivityStateRecord> com o estado de falha. A consulta correspondente é especificada no código a seguir.  
  
```xml  
<activityStateQueries>  
              <activityStateQuery activityName="*">  
                <states>  
                  <state name="Faulted" />  
                </states>  
              </activityStateQuery>  
 </activityStateQueries>  
```  
  
 Se uma falha é propagada e tratado em um manipulador de falha (como uma atividade de <xref:System.Activities.Statements.TryCatch> ) pode ser detectado usando <xref:System.Activities.Tracking.FaultPropagationRecord>. <xref:System.Activities.Tracking.FaultPropagationRecord> indica a atividade de origem de falha e o nome do manipulador de falha. O <xref:System.Activities.Tracking.FaultPropagationRecord> contém detalhes de falha na forma da pilha de exceção para a falha. A consulta para assinar um <xref:System.Activities.Tracking.FaultPropagationRecord> é mostrada no exemplo a seguir.  
  
```xml  
<faultPropagationQueries>  
              <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>  
 </faultPropagationQueries>  
```  
  
 Se uma falha não é tratada no fluxo de trabalho resulta em uma exceção não tratada na instância do fluxo de trabalho e a instância de fluxo de trabalho é anulada. Para entender os detalhes da exceção sem tratamento, o perfil de rastreamento deve consultar o registro de instância do fluxo de trabalho com o `state name="UnhandledException"` , conforme especificado no exemplo a seguir.  
  
```xml  
<workflowInstanceQueries>  
              <workflowInstanceQuery>  
                <states>  
                  <state name="UnhandledException" />  
                </states>  
              </workflowInstanceQuery>  
</workflowInstanceQueries>  
```  
  
 Quando uma instância de fluxo de trabalho encontra uma exceção sem tratamento, um <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord> objeto é emitido se o rastreamento de Windows Workflow Foundation tiver sido habilitado.  
  
 Esse registro de rastreamento contém os detalhes de falha na forma da pilha de exceção. Ele tem detalhes da origem da falha (por exemplo, a atividade) que falharam e resultaram na exceção sem tratamento. Para assinar eventos de falha de um Windows Workflow Foundation, habilite o acompanhamento adicionando um participante de controle. Configurar esse participante com um perfil de rastreamento que consultas para `ActivityStateQuery (state="Faulted")`, <xref:System.Activities.Tracking.FaultPropagationRecord>, e `WorkflowInstanceQuery (state="UnhandledException")`.  
  
 Se você estiver ativado usando o participante de rastreamento de ETW, os eventos de falha são emitidas a uma sessão de ETW. Eventos podem ser exibidos usando o visualizador de eventos do visualizador de eventos. Isso pode ser encontrado no nó **Visualizador de eventos->logs de aplicativos e serviços->Microsoft->Windows->Application Server – Applications** no canal analítico.  
  
## <a name="see-also"></a>Consulte também

- [Monitoramento do Windows Server app Fabric](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorando aplicativos com o app Fabric](/previous-versions/appfabric/ee677276(v=azure.10))
