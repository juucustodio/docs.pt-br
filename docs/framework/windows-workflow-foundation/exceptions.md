---
description: 'Saiba mais sobre: exceções'
title: Exceções
ms.date: 03/30/2017
ms.assetid: 065205cc-52dd-4f30-9578-b17d8d113136
ms.openlocfilehash: 71cf6a4ac23f7979d0c9137d88f36a45f71783a3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742446"
---
# <a name="exceptions"></a>Exceções

Fluxos de trabalho podem usar a atividade de <xref:System.Activities.Statements.TryCatch> para manipular exceções que são geradas durante a execução de um fluxo de trabalho. Essas exceções podem ser tratados ou que podem ser lançadas usando a atividade de <xref:System.Activities.Statements.Rethrow> . As atividades na seção de <xref:System.Activities.Statements.TryCatch.Finally%2A> são executadas quando a seção de <xref:System.Activities.Statements.TryCatch.Try%2A> ou a seção de <xref:System.Activities.Statements.TryCatch.Catches%2A> concluírem. Os fluxos de trabalho hospedados por uma <xref:System.Activities.WorkflowApplication> instância também podem usar o <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> manipulador de eventos para manipular exceções que não são tratadas por uma <xref:System.Activities.Statements.TryCatch> atividade.  
  
## <a name="causes-of-exceptions"></a>Causas de exceções  

 Em um fluxo de trabalho, exceções podem ser geradas das seguintes maneiras:  
  
- Um tempo limite de transações em <xref:System.Activities.Statements.TransactionScope>.  
  
- Uma exceção lançada explícita pelo fluxo de trabalho usando a atividade de <xref:System.Activities.Statements.Throw> .  
  
- Uma exceção lançada de [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] de uma atividade.  
  
- Uma exceção acionada de código externo, como bibliotecas, componentes, ou serviços que são usados no fluxo de trabalho.  
  
## <a name="handling-exceptions"></a>Tratando exceções  

 Se uma exceção é acionada por uma atividade e é não tratada, o comportamento padrão é finalizar a instância de fluxo de trabalho. Se um manipulador de <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> personalizado estiver presente, pode substituir esse comportamento padrão. Esse manipulador fornece o autor do host de fluxo de trabalho uma oportunidade para fornecer tratamento apropriado, como o log personalizado, anulando o fluxo de trabalho, cancelar o fluxo de trabalho, ou de terminação o fluxo de trabalho.  Se um fluxo de trabalho gerencie uma exceção que não é tratada, o manipulador de <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> é chamado. Há três ações possíveis retornadas de <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> que determinam o resultado final de fluxo de trabalho.  
  
- **Cancelar** -uma instância de fluxo de trabalho cancelada é uma saída normal de uma execução de ramificação. Você pode modelar o comportamento de cancelamento (por exemplo, usando uma atividade de CancellationScope). O manipulador concluído é chamado quando o processo de cancelamento completa. Um fluxo de trabalho cancelado está no estado cancelado.  
  
- **Término** -uma instância de fluxo de trabalho terminada não pode ser retomada ou reiniciada.  Isso dispara o evento concluído em que você pode fornecer uma exceção que a razão ele foi finalizada. O manipulador encerrado é chamado quando o processo de fim completa. Um fluxo de trabalho encerrado está no estado criticado.  
  
- **Anular** -uma instância de fluxo de trabalho anulada poderá ser retomada somente se tiver sido configurada para ser persistente.  Sem persistência, um fluxo de trabalho não pode ser continuado.  No ponto um fluxo de trabalho é anuladas, alguns funciona feito (na memória) como o ponto que o último de persistência será perdido. Para um fluxo de trabalho anuladas, o manipulador anuladas é chamado usando a exceção como a razão quando o processo de abort completa. No entanto, diferentemente de cancelado e de finalizado, o manipulador concluído não é chamado. Um fluxo de trabalho anuladas está em um estado anuladas.  
  
 O exemplo a seguir chama um fluxo de trabalho que gerencia uma exceção. A exceção é não tratados pelo fluxo de trabalho e o manipulador de <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> é chamado. <xref:System.Activities.WorkflowApplicationUnhandledExceptionEventArgs> é inspecionado para fornecer informações sobre a exceção, e fluxo de trabalho é encerrado.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1)]  
  
### <a name="handling-exceptions-with-the-trycatch-activity"></a>Manipulando exceções com a atividade de TryCatch  

 Manipulando exceções dentro de um fluxo de trabalho é executado pela atividade de <xref:System.Activities.Statements.TryCatch> . A atividade de <xref:System.Activities.Statements.TryCatch> tem uma coleção de <xref:System.Activities.Statements.TryCatch.Catches%2A> de atividades de <xref:System.Activities.Statements.Catch> que são associadas com um tipo específico de <xref:System.Exception> . Se a exceção acionada por uma atividade que está contida na seção de <xref:System.Activities.Statements.TryCatch.Try%2A> de uma atividade de <xref:System.Activities.Statements.TryCatch> corresponde a exceção de uma atividade de <xref:System.Activities.Statements.Catch%601> na coleção de <xref:System.Activities.Statements.TryCatch.Catches%2A> , então a exceção é tratada. Se a exceção é lançada novamente ou explicitamente uma nova exceção é lançada então passa essa exceção até a atividade pai. O exemplo de código a seguir mostra uma atividade de <xref:System.Activities.Statements.TryCatch> que manipula <xref:System.ApplicationException> que é gerada na seção de <xref:System.Activities.Statements.TryCatch.Try%2A> por uma atividade de <xref:System.Activities.Statements.Throw> . A mensagem de exceção é escrita para o console pela atividade de <xref:System.Activities.Statements.Catch%601> , e uma mensagem é gravada no console na seção de <xref:System.Activities.Statements.TryCatch.Finally%2A> .  
  
 [!code-csharp[CFX_WorkflowApplicationExample#33](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#33)]  
  
 As atividades na seção de <xref:System.Activities.Statements.TryCatch.Finally%2A> são executadas quando a seção de <xref:System.Activities.Statements.TryCatch.Try%2A> ou a seção de <xref:System.Activities.Statements.TryCatch.Catches%2A> completa com êxito. A seção de <xref:System.Activities.Statements.TryCatch.Try%2A> concluída com êxito se nenhuma exceção é lançada deles, e a seção de <xref:System.Activities.Statements.TryCatch.Catches%2A> concluída com êxito se nenhuma exceção é lançada ou rethrown deles. Se uma exceção é lançada na seção de <xref:System.Activities.Statements.TryCatch.Try%2A> de <xref:System.Activities.Statements.TryCatch> e não é tratada por <xref:System.Activities.Statements.Catch%601> na seção de <xref:System.Activities.Statements.TryCatch.Catches%2A> , nem é rethrown de <xref:System.Activities.Statements.TryCatch.Catches%2A>, as atividades em <xref:System.Activities.Statements.TryCatch.Finally%2A> não serão executadas a menos que o da seguir ocorrer.  
  
- A exceção é detectada por uma atividade de alto nível de <xref:System.Activities.Statements.TryCatch> no fluxo de trabalho, independentemente se é rethrown do <xref:System.Activities.Statements.TryCatch>de alto nível.  
  
- A exceção não é tratada por <xref:System.Activities.Statements.TryCatch>de alto nível, libera a raiz de trabalho, e o trabalho são configurados para cancelar em vez de finalizam ou exibe. Fluxos de trabalho usando <xref:System.Activities.WorkflowApplication> hospedados podem configurar esse manipulando <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> e retornando <xref:System.Activities.UnhandledExceptionAction.Cancel>. Um exemplo de manipular <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> é fornecido anteriormente neste tópico. Os serviços de fluxo de trabalho podem configurar isso usando <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> e especificando <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Cancel>. Para obter um exemplo de configuração <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> , consulte [extensibilidade do host do serviço de fluxo de trabalho](../wcf/feature-details/workflow-service-host-extensibility.md).  
  
## <a name="exception-handling-versus-compensation"></a>Manipulação de exceção com a compensação  

 A diferença entre a manipulação de exceção e a compensação é que a manipulação de exceção ocorre durante a execução de uma atividade. A compensação ocorre após uma atividade terminou com êxito. Manipulação de exceção fornece uma oportunidade para limpar após a atividade gerencie a exceção, enquanto a compensação fornece um mecanismo por que o trabalho com êxito concluído de uma atividade anteriormente pode ser concluída desfeito. Para obter mais informações, consulte [compensação](compensation.md).  
  
## <a name="see-also"></a>Confira também

- <xref:System.Activities.Statements.TryCatch>
- <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>
- <xref:System.Activities.Statements.CompensableActivity>
