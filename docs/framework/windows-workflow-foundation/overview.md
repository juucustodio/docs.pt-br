---
title: Visão geral de fluxo de trabalho do Windows
description: Este artigo descreve os fluxos de trabalho do Workflow Foundation, que são modelos que descrevem processos do mundo real.
ms.date: 03/30/2017
ms.assetid: fc44adbe-1412-49ae-81af-0298be44aae6
ms.openlocfilehash: f966aa2b62a743358d4c1ad18f237f988924014d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268671"
---
# <a name="windows-workflow-overview"></a>Visão geral de fluxo de trabalho do Windows

Um fluxo de trabalho é um conjunto de unidades elementas chamadas *atividades* que são armazenadas como um modelo que descreve um processo real. Fluxos de trabalho fornecem uma maneira de descrever a ordem de relações de execução e dependentes entre partes de trabalho ou longo tempo. Este trabalho passa pelo modelo do início ao final, e as atividades podem ser executadas por pessoas ou funções do sistema.  
  
## <a name="workflow-run-time-engine"></a>Mecanismo de fluxo de trabalho  

 Cada instância em execução de fluxo de trabalho é criado e mantido por um mecanismo em processo de tempo de execução que o processo host interage com o direto do seguinte:  
  
- <xref:System.Activities.WorkflowInvoker>, que chama o fluxo de trabalho como um método.  
  
- <xref:System.Activities.WorkflowApplication> para o controle explícito sobre a execução de uma única instância de fluxo de trabalho.  
  
- <xref:System.ServiceModel.WorkflowServiceHost> para interações mensagem- com base em cenários de várias instâncias.  
  
 Cada uma dessas classes envolve o runtime de atividade de núcleo representado como <xref:System.Activities.ActivityInstance> responsável pela atividade de execução. Pode haver vários objetos de <xref:System.Activities.ActivityInstance> dentro de um domínio de aplicativo executando simultaneamente.  
  
 Cada um dos três objetos de precedência de interação host é criado de uma árvore de atividades conhecido como um programa de fluxo de trabalho. Usando esses tipos ou um host personalizado que encapsula <xref:System.Activities.ActivityInstance> , os fluxos de trabalho podem ser executados dentro de qualquer processo do Windows, incluindo aplicativos de console, aplicativos baseados em formulários, serviços do Windows, sites da ASP.net e serviços do Windows Communication Foundation (WCF).  
  
 ![Componentes de fluxo de trabalho no processo do host](./media/44c79d1d-178b-4487-87ed-3e33015a3842.gif "44c79d1d-178b-4487-87ed-3e33015a3842")  
Componentes de fluxo de trabalho no processo do host  
  
## <a name="interaction-between-workflow-components"></a>Interação entre componentes de fluxo de trabalho  

 O diagrama a seguir demonstra como os componentes de fluxo de trabalho interagem um com o outro.  
  
 ![Diagrama que mostra como os componentes de fluxo de trabalho interagem.](./media/overview/workflow-component-interatction.gif)  
  
 No diagrama anterior, o método de <xref:System.Activities.WorkflowInvoker.Invoke%2A> da classe de <xref:System.Activities.WorkflowInvoker> é usado para chamar várias instâncias de fluxo de trabalho. <xref:System.Activities.WorkflowInvoker> é usado para fluxos de trabalho leve que não precisam o gerenciamento de host; fluxos de trabalho que precisam o gerenciamento de host (como a ressunção de <xref:System.Activities.Bookmark> ) devem ser executados usando <xref:System.Activities.WorkflowApplication.Run%2A> em vez disso. Não é necessário esperar uma instância de fluxo de trabalho para terminar antes de chamar outra; suporte de mecanismo de runtime que executam várias o fluxo de trabalho instância como exemplo simultaneamente.  Fluxos de trabalho são chamados como segue:  
  
- Uma atividade de <xref:System.Activities.Statements.Sequence> que contém uma atividade do filho de <xref:System.Activities.Statements.WriteLine> . <xref:System.Activities.Variable> de atividade pai é associado a <xref:System.Activities.InArgument> de atividade filho. Para obter mais informações sobre variáveis, argumentos e associação, consulte [variáveis e argumentos](variables-and-arguments.md).  
  
- Uma atividade `ReadLine`personalizado chamado. <xref:System.Activities.OutArgument> de atividade de `ReadLine` é retornado para o método chamando de <xref:System.Activities.WorkflowInvoker.Invoke%2A> .  
  
- Uma atividade personalizada que derive da classe abstrata de <xref:System.Activities.CodeActivity> . <xref:System.Activities.CodeActivity> pode acessar os recursos de tempo de execução (como o rastreamento e as propriedades) que usam <xref:System.Activities.CodeActivityContext> que está disponível como um parâmetro do método de <xref:System.Activities.CodeActivity.Execute%2A> . Para obter mais informações sobre esses recursos de tempo de execução, consulte rastreamento de [fluxo de trabalho e](workflow-tracking-and-tracing.md) [Propriedades de execução de fluxo](workflow-execution-properties.md)de trabalho.  
  
## <a name="see-also"></a>Veja também

- [BizTalk Server 2006 ou WF? Escolhendo a ferramenta de fluxo de trabalho certa para seu projeto](/previous-versions/dotnet/articles/cc303238(v=msdn.10))
