---
title: Usando WorkflowInvoker e WorkflowApplication
description: Este artigo descreve a hospedagem de fluxo de trabalho usando WorkflowInvoker e WorkflowApplication no Windows Workflow Foundation.
ms.date: 03/30/2017
ms.assetid: cd0e583c-a3f9-4fa2-b247-c7b3368c48a7
ms.openlocfilehash: 1cc84afe002615c317309054179abd1af5800e9c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254604"
---
# <a name="using-workflowinvoker-and-workflowapplication"></a>Usando WorkflowInvoker e WorkflowApplication

Windows Workflow Foundation (WF) fornece vários métodos de Hospedagem de fluxos de trabalho. <xref:System.Activities.WorkflowInvoker> fornece uma maneira simples para chamar um fluxo de trabalho como se fosse uma chamada de método e pode ser usado somente para os fluxos de trabalho que não usam persistência. <xref:System.Activities.WorkflowApplication> fornece um modelo mais rico para executar fluxos de trabalho que inclui notificação de eventos de ciclo de vida, controle de execução, de ressunção do indexador, e de persistência. <xref:System.ServiceModel.Activities.WorkflowServiceHost> fornece suporte para atividades de mensagem e é basicamente usado com serviços de fluxo de trabalho. Este tópico apresenta o fluxo de trabalho que hospeda com <xref:System.Activities.WorkflowInvoker> e <xref:System.Activities.WorkflowApplication>. Para obter mais informações sobre como hospedar fluxos de trabalho com o <xref:System.ServiceModel.Activities.WorkflowServiceHost> , consulte [serviços de fluxo](../wcf/feature-details/workflow-services.md) de trabalho e [serviços de fluxo de trabalho de hospedagem](../wcf/feature-details/hosting-workflow-services-overview.md).  
  
## <a name="using-workflowinvoker"></a>Usando WorkflowInvoker  

 <xref:System.Activities.WorkflowInvoker> fornece um modelo para executar um fluxo de trabalho como se fosse um chamada de método. Para chamar um fluxo de trabalho usando <xref:System.Activities.WorkflowInvoker>, chame o método de <xref:System.Activities.WorkflowInvoker.Invoke%2A> e passe a definição de fluxo de trabalho de fluxo de trabalho para chamar. Nesse exemplo, uma atividade de <xref:System.Activities.Statements.WriteLine> é chamada usando <xref:System.Activities.WorkflowInvoker>.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#1)]  
  
 Quando um fluxo de trabalho é chamado usando <xref:System.Activities.WorkflowInvoker>, o fluxo de trabalho é executado no segmento de chamada e os blocos de método <xref:System.Activities.WorkflowInvoker.Invoke%2A> até que o fluxo de trabalho está completo, incluindo qualquer tempo ocioso. Para configurar um intervalo de tempo limite em que o fluxo de trabalho deveria concluir, use uma das sobrecargas de <xref:System.Activities.WorkflowInvoker.Invoke%2A> que usa um parâmetro de <xref:System.TimeSpan> . Nesse exemplo, um fluxo de trabalho é chamado duas vezes em com dois intervalos de tempo limite diferentes. Os primeiros complets de fluxo de trabalho, mas os segundos não.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#50](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#50)]  
  
> [!NOTE]
> <xref:System.TimeoutException> é acionada somente se o intervalo de tempo limite decorre e fluxo de trabalho se torna ocioso durante a execução. Um fluxo de trabalho que recebe mais tempo do intervalo de tempo limite especificado para concluir concluída com êxito se o fluxo de trabalho não se torna ocioso.  
  
 <xref:System.Activities.WorkflowInvoker> também fornece versões assíncronas do método invoke. Para obter mais informações, consulte <xref:System.Activities.WorkflowInvoker.InvokeAsync%2A> e <xref:System.Activities.WorkflowInvoker.BeginInvoke%2A>.  
  
### <a name="setting-input-arguments-of-a-workflow"></a>Argumentos de entrada de configuração de um fluxo de trabalho  

 Os dados podem ser passados em um fluxo de trabalho usando um dicionário de parâmetros de entrada, fechado pelo nome de argumento, que mapeiam para argumentos de entrada de fluxo de trabalho. Nesse exemplo, <xref:System.Activities.Statements.WriteLine> é chamado e o valor para o argumento de <xref:System.Activities.Statements.WriteLine.Text%2A> é especificado usando o dicionário de parâmetros.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#3](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#3)]  
  
### <a name="retrieving-output-arguments-of-a-workflow"></a>Recuperando argumentos de saída de um fluxo de trabalho  

 Parâmetros de saída de um fluxo de trabalho podem ser obtidos usando o dicionário de saída que é retornado da chamada a <xref:System.Activities.WorkflowInvoker.Invoke%2A>. O exemplo a seguir chama um fluxo de trabalho que consiste em uma única atividade de `Divide` que tem dois argumentos conectados e dois argumentos de saída. Quando o fluxo de trabalho é chamado, o dicionário de `arguments` é passado que contém os valores para cada argumento de entrada, fechado pelo nome do argumento. Quando o `Invoke` a chamada retorna, cada argumento de saída é retornado no dicionário de `outputs` , também fechado pelo nome do argumento.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#120](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#120)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#20](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#20)]  
  
 Se o fluxo de trabalho deriva de <xref:System.Activities.ActivityWithResult>, como `CodeActivity<TResult>` ou `Activity<TResult>`, e há argumentos de saída além do argumento bem definido de saída de <xref:System.Activities.Activity%601.Result%2A> , uma sobrecarga não genérico de `Invoke` deve ser usada para recuperar os argumentos adicionais. Para fazer isso, a definição de fluxo de trabalho passada em `Invoke` deve ser do tipo <xref:System.Activities.Activity>. Nesse exemplo a atividade de `Divide` deriva de `CodeActivity<int>`, mas é declarada como <xref:System.Activities.Activity> de modo que uma sobrecarga não genérico de `Invoke` é usada que retorna um dicionário dos argumentos em vez de um único valor de retorno.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#121](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#121)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#21](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#21)]  
  
## <a name="using-workflowapplication"></a>Usando WorkflowApplication  

 <xref:System.Activities.WorkflowApplication> fornece um conjunto rico de recursos para gerenciamento de instância de fluxo de trabalho. <xref:System.Activities.WorkflowApplication> atua como um proxy segura do que a <xref:System.Activities.Hosting.WorkflowInstance>real, que encapsula o runtime, e fornece métodos para criar e carregar instâncias de fluxo de trabalho, pausar e continuar-las, finalizar, e notificação de eventos de ciclo de vida. Para executar um fluxo de trabalho usando <xref:System.Activities.WorkflowApplication> que você cria <xref:System.Activities.WorkflowApplication>, assinar os eventos desejados do ciclo de vida, a inicia o fluxo de trabalho, e espera-o em concluir. Nesse exemplo, uma definição de fluxo de trabalho que consiste em uma atividade de <xref:System.Activities.Statements.WriteLine> é criada e <xref:System.Activities.WorkflowApplication> são criados usando a definição especificada de fluxo de trabalho. <xref:System.Activities.WorkflowApplication.Completed%2A> é tratado para que o host é notificado quando o fluxo de trabalho for concluída, o fluxo de trabalho é iniciado com uma chamada a <xref:System.Activities.WorkflowApplication.Run%2A>, e então o host espera o fluxo de trabalho para concluir. Quando o fluxo de trabalho terminar, <xref:System.Threading.AutoResetEvent> é ajustado e o aplicativo host pode continuar a execução, conforme mostrado no exemplo o seguir.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#31](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#31)]  
  
### <a name="workflowapplication-lifecycle-events"></a>Eventos de ciclo de vida de WorkflowApplication  

 Além de <xref:System.Activities.WorkflowApplication.Completed%2A>, os autores de host podem ser notificados quando um fluxo de trabalho é descarregado (<xref:System.Activities.WorkflowApplication.Unloaded%2A>), anuladas (<xref:System.Activities.WorkflowApplication.Aborted%2A>), se torna ocioso (<xref:System.Activities.WorkflowApplication.Idle%2A> e <xref:System.Activities.WorkflowApplication.PersistableIdle%2A>), ou uma exceção não manipulada ocorre (<xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>). Os desenvolvedores de aplicativos de fluxo de trabalho podem tratar essas notificações e a ação apropriada, conforme mostrado no exemplo o seguir.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#32](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#32)]  
  
### <a name="setting-input-arguments-of-a-workflow"></a>Argumentos de entrada de configuração de um fluxo de trabalho  

 Os dados podem ser passados em um fluxo de trabalho como são iniciados usar um dicionário de parâmetros, semelhante à forma que os dados são passados na o usar <xref:System.Activities.WorkflowInvoker>. Cada item em mapas de dicionário para um argumento de entrada de fluxo de trabalho especificado. Nesse exemplo, um fluxo de trabalho que consiste em uma atividade de <xref:System.Activities.Statements.WriteLine> é chamado e o argumento de <xref:System.Activities.Statements.WriteLine.Text%2A> são especificados usando o dicionário de parâmetros.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#30](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#30)]  
  
### <a name="retrieving-output-arguments-of-a-workflow"></a>Recuperando argumentos de saída de um fluxo de trabalho  

 Quando um fluxo de trabalho concluir, os argumentos de saída podem ser recuperados no manipulador de <xref:System.Activities.WorkflowApplication.Completed%2A> acessando o dicionário de <xref:System.Activities.WorkflowApplicationCompletedEventArgs.Outputs%2A?displayProperty=nameWithType> . O exemplo a seguir hospeda um fluxo de trabalho usando <xref:System.Activities.WorkflowApplication>. Uma <xref:System.Activities.WorkflowApplication> instância é construída usando uma definição de fluxo de trabalho que consiste em uma única `DiceRoll` atividade. A atividade de `DiceRoll` tem dois argumentos de saída que representam os resultados da operação de rolagem de dados. Quando o fluxo de trabalho for concluído, a saída são recuperadas no manipulador de <xref:System.Activities.WorkflowApplication.Completed%2A> .  
  
 [!code-csharp[CFX_WorkflowApplicationExample#130](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#130)]  
  
 [!code-csharp[CFX_WorkflowApplicationExample#21](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#21)]  
  
> [!NOTE]
> <xref:System.Activities.WorkflowApplication> e <xref:System.Activities.WorkflowInvoker> têm um dicionário de argumentos de entrada e retornam um dicionário de argumentos de `out` . Esses parâmetros, propriedades, e valores de retorno do dicionário são do tipo `IDictionary<string, object>`. A instância real da classe dicionário que é passada em pode ser qualquer classe que implemente `IDictionary<string, object>`. Nesses exemplos, `Dictionary<string, object>` é usado. Para obter mais informações sobre dicionários, consulte <xref:System.Collections.Generic.IDictionary%602> e <xref:System.Collections.Generic.Dictionary%602> .  
  
### <a name="passing-data-into-a-running-workflow-using-bookmarks"></a>Passando dados em um fluxo de trabalho em execução usando indicadores  

 Indexadores são o mecanismo por que uma atividade passiva pode esperar para ser continuado e é um mecanismo para passar dados em uma instância em execução de fluxo de trabalho. Se uma atividade está aguardando dados, <xref:System.Activities.Bookmark> pode criar e registrar um método callback a ser chamado quando <xref:System.Activities.Bookmark> é que, conforme mostrado no exemplo o seguir.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
 Quando executada, a atividade de `ReadLine` cria <xref:System.Activities.Bookmark>, registra um retorno de chamada, e espera em <xref:System.Activities.Bookmark> a ser continuado. Quando é continuada, a atividade de `ReadLine` atribui os dados que foram passados com <xref:System.Activities.Bookmark> ao seu argumento de <xref:System.Activities.Activity%601.Result%2A> . Nesse exemplo, um fluxo de trabalho é criado que usa a atividade de `ReadLine` para coletar o nome de usuário e para o exibir a janela do console.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#22](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#22)]  
  
 Quando a atividade de `ReadLine` é executada, cria <xref:System.Activities.Bookmark> chamado `UserName` e espera no indexador a ser continuado. O host reúne os dados desejados e depois <xref:System.Activities.Bookmark>. Retoma de fluxo de trabalho, exibe o nome, e então usa.  
  
 O aplicativo host pode inspecionar o fluxo de trabalho para determinar se houver qualquer marcador ativo. Pode fazer isso chamando o método de <xref:System.Activities.WorkflowApplication.GetBookmarks%2A> de uma instância de <xref:System.Activities.WorkflowApplication> , ou inspecionando <xref:System.Activities.WorkflowApplicationIdleEventArgs> no manipulador de <xref:System.Activities.WorkflowApplication.Idle%2A> .  
  
 O exemplo de código é como o exemplo anterior exceto que os indicadores ativas são enumerados antes que o indexador é continuado. O fluxo de trabalho é iniciado, e depois que <xref:System.Activities.Bookmark> é criado e fluxo de trabalho aparece ociosa, <xref:System.Activities.WorkflowApplication.GetBookmarks%2A> é chamado. Quando o fluxo de trabalho for concluído, a saída a seguir são exibidas no console.  
  
 **Que é o nome?**  
**BookmarkName: username-OwnerDisplayName: ReadLine** 
 **Steve** 
 **Olá, Steve**

[!code-csharp[CFX_WorkflowApplicationExample#14](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#14)]  
  
 O exemplo de código inspeciona <xref:System.Activities.WorkflowApplicationIdleEventArgs> passado para o manipulador de <xref:System.Activities.WorkflowApplication.Idle%2A> de uma instância de <xref:System.Activities.WorkflowApplication> . Nesse exemplo a ociosa indo de fluxo de trabalho tem um <xref:System.Activities.Bookmark> com um nome de `EnterGuess`, possuídas por uma atividade chamada `ReadInt`. Este exemplo de código se baseia em [como: executar um fluxo de trabalho](how-to-run-a-workflow.md), que faz parte do [tutorial de introdução](getting-started-tutorial.md). Se o manipulador de <xref:System.Activities.WorkflowApplication.Idle%2A> nessa etapa é alterado para conter o código deste exemplo, a seguinte saída são exibidas.  
  
 **BookmarkName: EnterGuess - OwnerDisplayName: ReadInt**

 [!code-csharp[CFX_WorkflowApplicationExample#2](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#2)]  
  
## <a name="summary"></a>Resumo  

 <xref:System.Activities.WorkflowInvoker> fornece uma maneira leve de invocar fluxos de trabalho e, embora fornece métodos para passar dados no início de um fluxo de trabalho e extrair dados de um fluxo de trabalho concluído, não fornece cenários mais complexos que é onde <xref:System.Activities.WorkflowApplication> pode ser usado.
