---
description: 'Saiba mais sobre: comportamento de cancelamento de modelagem em fluxos de trabalho'
title: Modelando o comportamento cancelar em fluxos de trabalho
ms.date: 03/30/2017
ms.assetid: d48f6cf3-cdde-4dd3-8265-a665acf32a03
ms.openlocfilehash: 971e044336eb0aed41e773e03f6e0fb70d959094
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792642"
---
# <a name="modeling-cancellation-behavior-in-workflows"></a>Modelando o comportamento cancelar em fluxos de trabalho

As atividades podem ser canceladas em um fluxo de trabalho, por exemplo por uma atividade de <xref:System.Activities.Statements.Parallel> que cancela ramificações incompletos quando seu <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> avalia a `true`, ou fora de fluxo de trabalho, se o host chama <xref:System.Activities.WorkflowApplication.Cancel%2A>. Para fornecer tratamento cancelar, os autores de fluxo de trabalho podem usar a atividade de <xref:System.Activities.Statements.CancellationScope> , a atividade de <xref:System.Activities.Statements.CompensableActivity> , ou crie as atividades personalizados que fornecem lógica cancelar. Este tópico fornece uma visão geral de cancelamento em fluxos de trabalho.  
  
## <a name="cancellation-compensation-and-transactions"></a>Cancelar, compensação, e transações  

 As transações fornecem ao seu aplicativo a capacidade de nulo () para reverter as alterações executadas dentro de transação se qualquer erro ocorre durante qualquer parte do processo de transação. No entanto, nem todo o trabalho que precise ser cancelado ou desfeito é apropriado para transações, como o trabalho longo ou o trabalho que não envolvem recursos transacionais. A compensação fornece um modelo para desfazer o trabalho não transacional anteriormente concluído se houver uma falha subsequente no fluxo de trabalho. Cancelamento fornece um modelo para autores de fluxo de trabalho e atividade do trabalho não transacional de forma que não foi concluído. Se uma atividade não concluiu sua execução e será cancelada, sua lógica cancelar será chamada está disponível.  
  
> [!NOTE]
> Para obter mais informações sobre transações e compensação, consulte [Transações](workflow-transactions.md) e [remuneração](compensation.md).  
  
## <a name="using-cancellationscope"></a>Usando CancellationScope  

 A atividade de <xref:System.Activities.Statements.CancellationScope> tem duas seções que podem conter atividades filhos: <xref:System.Activities.Statements.CancellationScope.Body%2A> e <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>. <xref:System.Activities.Statements.CancellationScope.Body%2A> é onde as atividades que compõem a lógica de atividade são colocadas, e <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> é onde as atividades que fornecem lógica cancelar para atividades são colocadas. Uma atividade pode ser cancelada somente se não tiver concluído. No caso de atividade de <xref:System.Activities.Statements.CancellationScope> , o preenchimento refere-se a conclusão de atividades em <xref:System.Activities.Statements.CancellationScope.Body%2A>. Se uma solicitação cancelar é agendada e as atividades em <xref:System.Activities.Statements.CancellationScope.Body%2A> não tiverem terminado, então <xref:System.Activities.Statements.CancellationScope> será marcado como <xref:System.Activities.ActivityInstanceState.Canceled> e as atividades de <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> serão executadas.  
  
### <a name="canceling-a-workflow-from-the-host"></a>Cancelando um fluxo de trabalho do host  

 Um host pode cancelar um fluxo de trabalho chamando o método <xref:System.Activities.WorkflowApplication.Cancel%2A> de instância de <xref:System.Activities.WorkflowApplication> que está hospedando o fluxo de trabalho. No exemplo a seguir um fluxo de trabalho é criado que tem <xref:System.Activities.Statements.CancellationScope>. O fluxo de trabalho é chamado, e então o host uma chamada a <xref:System.Activities.WorkflowApplication.Cancel%2A>. A execução do fluxo de trabalho é interrompida, <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> de <xref:System.Activities.Statements.CancellationScope> é chamado, e então o fluxo de trabalho termina com um status de <xref:System.Activities.ActivityInstanceState.Canceled>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#35](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#35)]  
  
 Quando esse fluxo de trabalho é chamado, a seguinte saída é exibida no console.  
  
 **Iniciando o fluxo de trabalho.**  
**CancellationHandler invocado.** 
 **B30ebb30-df46-4d90-A211-e31c38d8db3c de fluxo de trabalho cancelado.**
> [!NOTE]
> Quando uma atividade de <xref:System.Activities.Statements.CancellationScope> é cancelada e <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> é invocado, foi responsabilidade do autor de fluxo de trabalho determinar o progresso que a atividade cancelada feita antes que foi cancelado para fornecer a lógica apropriada cancelar. <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> não fornece nenhuma informação sobre o andamento de atividade cancelada.  
  
 Um fluxo de trabalho também pode ser cancelado host se uma exceção não tratada borbulha anterior após a raiz de fluxo de trabalho e o manipulador de <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> retorna <xref:System.Activities.UnhandledExceptionAction.Cancel>. Nesse exemplo inicia o fluxo de trabalho e lançam em <xref:System.ApplicationException>. Esta exceção é não tratados pelo fluxo de trabalho e então o manipulador de <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> é chamado. O manipulador instrui o runtime para cancelar o fluxo de trabalho, e <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> atividade estão atualmente em execução de <xref:System.Activities.Statements.CancellationScope> é chamado.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#36](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#36)]  
  
 Quando esse fluxo de trabalho é chamado, a seguinte saída é exibida no console.  
  
 **Iniciando o fluxo de trabalho.**  
**OnUnhandledException no fluxo de trabalho 6bb2d5d6-f49a-4C6D-a988-478afb86dbe9** 
 **Uma ApplicationException foi gerada.** 
 **CancellationHandler invocado.** 
 **6bb2d5d6-f49a-4C6D-a988-478afb86dbe9 de fluxo de trabalho cancelado.**

### <a name="canceling-an-activity-from-inside-a-workflow"></a>Cancelando uma atividade de dentro de um fluxo de trabalho  

 Uma atividade também pode ser cancelada por seu pai. Por exemplo, se uma atividade de <xref:System.Activities.Statements.Parallel> tem várias ramificações e que executa o <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> avalia a `true` suas ramificações incompletos serão canceladas em seguida. Nesse exemplo uma atividade de <xref:System.Activities.Statements.Parallel> é criada que possui duas ramificações. O <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> é definido como `true` portanto <xref:System.Activities.Statements.Parallel> concluir o que qualquer uma de suas ramificações terminar. Nesta ramificação 2 do exemplo completo, e assim que a 1 é cancelado.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#37](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#37)]  
  
 Quando esse fluxo de trabalho é chamado, a seguinte saída é exibida no console.  
  
 **Ramificação 1 que inicia.**  
**Ramificação 2 concluída.** 
 **Ramificação 1 cancelada.** 
 **E0685e24-18ef-4A47-acf3-5c638732f3be de fluxo de trabalho concluído.**  As atividades também são canceladas se uma exceção borbulha anterior após a raiz da atividade mas tratadas em um nível mais alto no fluxo de trabalho. Nesse exemplo, a principal lógica de fluxo de trabalho consiste em uma atividade de <xref:System.Activities.Statements.Sequence> . <xref:System.Activities.Statements.Sequence> é especificado como <xref:System.Activities.Statements.CancellationScope.Body%2A> de uma atividade de <xref:System.Activities.Statements.CancellationScope> que está contida por uma atividade de <xref:System.Activities.Statements.TryCatch> . Uma exceção é lançada do corpo de <xref:System.Activities.Statements.Sequence>, é tratada pela atividade pai de <xref:System.Activities.Statements.TryCatch> , e <xref:System.Activities.Statements.Sequence> é cancelado.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#39](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#39)]  
  
 Quando esse fluxo de trabalho é chamado, a seguinte saída é exibida no console.  
  
 **Iniciar a sequência.**  
**Sequência cancelada.** 
 **Exceção detectada.** 
 **E3c18939-121e-4c43-af1c-ba1ce977ce55 de fluxo de trabalho concluído.**

### <a name="throwing-exceptions-from-a-cancellationhandler"></a>Gerar exceções de um CancellationHandler  

 Todas as exceções geradas de <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> de <xref:System.Activities.Statements.CancellationScope> são fatais ao fluxo de trabalho. Se houver uma chance de exceções que escapam de <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>, use <xref:System.Activities.Statements.TryCatch> em <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> para capturar e tratar essas exceções.  
  
### <a name="cancellation-using-compensableactivity"></a>Cancelar usando CompensableActivity  

 Como a atividade de <xref:System.Activities.Statements.CancellationScope> , <xref:System.Activities.Statements.CompensableActivity> tem <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>. Se <xref:System.Activities.Statements.CompensableActivity> é cancelado, todas as atividades em seu <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> são chamadas. Isso pode ser útil para desfazer o trabalho compensável parcialmente concluído. Para obter informações sobre como usar <xref:System.Activities.Statements.CompensableActivity> para compensação e cancelamento, consulte [compensação](compensation.md).  
  
## <a name="cancellation-using-custom-activities"></a>Cancelar usando atividades personalizados  

 Os autores de atividade personalizados podem implementar a lógica cancelar nas atividades personalizados em várias maneiras diferentes. As atividades personalizados que derivam de <xref:System.Activities.Activity> podem implementar a lógica de cancelamento colocando <xref:System.Activities.Statements.CancellationScope> ou outra atividade personalizado que contém a lógica cancelar no corpo da atividade. <xref:System.Activities.AsyncCodeActivity> e as atividades <xref:System.Activities.NativeActivity> derivadas podem substituir o método respectivo de <xref:System.Activities.NativeActivity.Cancel%2A> e fornecer a lógica de cancelamento lá. <xref:System.Activities.CodeActivity> derivado atividades não fornece nenhuma para o cancelamento como todo o trabalho é executado em uma única explosão de execução quando o runtime chama o método de <xref:System.Activities.CodeActivity.Execute%2A> . Se o método executar não foi chamado ainda e uma atividade com base <xref:System.Activities.CodeActivity> será cancelada, a atividade fecha com um status de <xref:System.Activities.ActivityInstanceState.Canceled> e o método de <xref:System.Activities.CodeActivity.Execute%2A> não é chamado.  
  
### <a name="cancellation-using-nativeactivity"></a>Cancelar usando NativeActivity  

 <xref:System.Activities.NativeActivity> derivado atividades pode substituir o método de <xref:System.Activities.NativeActivity.Cancel%2A> para fornecer a lógica personalizada cancelar. Se este método não é substituído, então a lógica padrão de cancelamento de fluxo de trabalho é aplicada. O cancelamento padrão é o processo que ocorre para um <xref:System.Activities.NativeActivity> que não substitui o <xref:System.Activities.NativeActivity.Cancel%2A> método ou cujo <xref:System.Activities.NativeActivity.Cancel%2A> método chama o <xref:System.Activities.NativeActivity> <xref:System.Activities.NativeActivity.Cancel%2A> método base. Quando uma atividade é cancelada, o runtime sinaliza a atividade para o botão e automaticamente trata determinada limpeza. Se a atividade tem apenas indicadores pendentes, os indicadores serão removidos e a atividade será marcada como <xref:System.Activities.ActivityInstanceState.Canceled>. Todas as atividades filhos excelentes de atividade cancelada serão canceladas por sua vez. Qualquer tentativa de agendar atividades filho adicionais resultará na tentativa que está sendo ignorada e a atividade será marcada como <xref:System.Activities.ActivityInstanceState.Canceled>. Se alguma atividade excelente filho termina em <xref:System.Activities.ActivityInstanceState.Canceled> ou estado de <xref:System.Activities.ActivityInstanceState.Faulted> , então a atividade será marcada como <xref:System.Activities.ActivityInstanceState.Canceled>. Observe que uma solicitação de cancelamento pode ser ignorada. Se uma atividade não tem nenhum indicadores pendentes ou executar atividades filhos e não agenda os itens de trabalho adicionais após o embandeiramento para cancelamento, se concluirá com êxito. Este padrão cancelar basta para muitos cenários, mas se a lógica adicional cancelar é necessária, então as atividades internos de cancelamento ou as atividades personalizados podem ser usadas.  
  
 No exemplo a seguir, a substituição de <xref:System.Activities.NativeActivity.Cancel%2A> de uma atividade personalizada com base <xref:System.Activities.NativeActivity> de `ParallelForEach` é definida. Quando a atividade é cancelada, alças desta substituição lógica cancelar para atividades. Este exemplo faz parte do exemplo de [ParallelForEach não genérico](./samples/non-generic-parallelforeach.md) .  
  
```csharp  
protected override void Cancel(NativeActivityContext context)  
{  
    // If we do not have a completion condition then we can just  
    // use default logic.  
    if (this.CompletionCondition == null)  
    {  
        base.Cancel(context);  
    }  
    else  
    {  
        context.CancelChildren();  
    }  
}  
```  
  
 <xref:System.Activities.NativeActivity> derivado atividades pode determinar se o cancelar foi solicitado inspecionando a propriedade de <xref:System.Activities.NativeActivityContext.IsCancellationRequested%2A> , e marcar-se como canceladas chamando o método <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> . A chamada <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> não concluir imediatamente a atividade. Como de costume, o runtime se concluirá a atividade quando não tem não mais trabalho excelente, mas se <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> é chamado estado final será <xref:System.Activities.ActivityInstanceState.Canceled> em vez de <xref:System.Activities.ActivityInstanceState.Closed>.  
  
### <a name="cancellation-using-asynccodeactivity"></a>Cancelar usando AsyncCodeActivity  

 <xref:System.Activities.AsyncCodeActivity> com atividades também pode fornecer a lógica personalizada cancelar substituindo o método de <xref:System.Activities.AsyncCodeActivity.Cancel%2A> . Se este método não é substituído, então nenhuma tratamento cancelar é executada se a atividade é cancelada. No exemplo a seguir, a substituição de <xref:System.Activities.AsyncCodeActivity.Cancel%2A> de uma atividade personalizada com base <xref:System.Activities.AsyncCodeActivity> de `ExecutePowerShell` é definida. Quando a atividade é cancelada, executa o comportamento desejado cancelar.
  
 [!code-csharp[CFX_WorkflowApplicationExample#1020](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1020)]  
  
 <xref:System.Activities.AsyncCodeActivity> derivado atividades pode determinar se o cancelar foi solicitado inspecionando a propriedade de <xref:System.Activities.AsyncCodeActivityContext.IsCancellationRequested%2A> , e marcar-se como canceladas chamando o método <xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A> .
