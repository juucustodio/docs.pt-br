---
description: 'Saiba mais sobre: indicadores'
title: Indicadores-WF
ms.date: 03/30/2017
ms.assetid: 9b51a346-09ae-455c-a70a-e2264ddeb9e2
ms.openlocfilehash: b4f0e68e0868ecd4eb97673ff6c09ee8c806cf43
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787923"
---
# <a name="bookmarks"></a>Indicadores

Indexadores são o mecanismo que permite uma atividade para esperar passiva entrada sem conter um segmento de fluxo de trabalho. Quando uma atividade sinaliza que está esperando estímulo, pode criar um indexador. Isso indica o runtime que a execução da atividade não deve ser considerada completo mesmo quando o método atualmente em execução (que criou <xref:System.Activities.Bookmark>) retorna.  
  
## <a name="bookmark-basics"></a>Noções básicas do indexador  

 <xref:System.Activities.Bookmark> representa um ponto em que a execução pode ser continuada (e através de entrada que pode ser entregada) em uma instância de fluxo de trabalho. Normalmente, <xref:System.Activities.Bookmark> é dado um nome e host (ou extensão) o código externo é responsável para continuar o indexador com dados relevantes. Quando <xref:System.Activities.Bookmark> é que, o runtime de fluxo de trabalho agenda o representante de <xref:System.Activities.BookmarkCallback> que foi associado com esse <xref:System.Activities.Bookmark> na altura do projeto.  
  
## <a name="bookmark-options"></a>Opções do indexador  

 A classe de <xref:System.Activities.BookmarkOptions> especifica o tipo de <xref:System.Activities.Bookmark> que está sendo criado. Os valores não mutuamente exclusivos possíveis são <xref:System.Activities.BookmarkOptions.None>, <xref:System.Activities.BookmarkOptions.MultipleResume>, e <xref:System.Activities.BookmarkOptions.NonBlocking>. Use <xref:System.Activities.BookmarkOptions.None>, a opção, ao criar <xref:System.Activities.Bookmark> que seja continuada exatamente uma vez. Use <xref:System.Activities.BookmarkOptions.MultipleResume> ao criar <xref:System.Activities.Bookmark> que pode ser que várias vezes. Use <xref:System.Activities.BookmarkOptions.NonBlocking> ao criar <xref:System.Activities.Bookmark> que pode ser que nunca. Ao contrário dos indicadores criados usando <xref:System.Activities.BookmarkOptions>padrão, os indicadores de <xref:System.Activities.BookmarkOptions.NonBlocking> não impede que uma atividade terminar.  
  
## <a name="bookmark-resumption"></a>Ressunção do indexador  

 Indexadores podem ser continuados pelo código fora de um fluxo de trabalho usando uma das sobrecargas de <xref:System.Activities.WorkflowApplication.ResumeBookmark%2A> . Nesse exemplo, uma atividade de `ReadLine` é criada. Quando executada, a atividade de `ReadLine` cria <xref:System.Activities.Bookmark>, registra um retorno de chamada, e espera em <xref:System.Activities.Bookmark> a ser continuado. Quando é continuada, a atividade de `ReadLine` atribui os dados que foram passados com <xref:System.Activities.Bookmark> ao seu argumento de <xref:System.Activities.Activity%601.Result%2A> .  
  
```csharp  
public sealed class ReadLine : NativeActivity<string>  
{  
    [RequiredArgument]  
    public  InArgument<string> BookmarkName { get; set; }  
  
    protected override void Execute(NativeActivityContext context)  
    {  
        // Create a Bookmark and wait for it to be resumed.  
        context.CreateBookmark(BookmarkName.Get(context),
            new BookmarkCallback(OnResumeBookmark));  
    }  
  
    // NativeActivity derived activities that do asynchronous operations by calling
    // one of the CreateBookmark overloads defined on System.Activities.NativeActivityContext
    // must override the CanInduceIdle property and return true.  
    protected override bool CanInduceIdle  
    {  
        get { return true; }  
    }  
  
    public void OnResumeBookmark(NativeActivityContext context, Bookmark bookmark, object obj)  
    {  
        // When the Bookmark is resumed, assign its value to  
        // the Result argument.  
        Result.Set(context, (string)obj);  
    }  
}  
```  
  
 Nesse exemplo, um fluxo de trabalho é criado que usa a atividade de `ReadLine` para coletar o nome de usuário e para o exibir a janela do console. O aplicativo host executa o trabalho real de coletar entrada e passá-lo para o fluxo de trabalho continuando <xref:System.Activities.Bookmark>.  
  
```csharp  
Variable<string> name = new Variable<string>  
{  
    Name = "name"  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        name  
    },  
    Activities =  
    {  
        new WriteLine()  
        {  
            Text = "What is your name?"  
        },  
        new ReadLine()  
        {  
            BookmarkName = "UserName",  
            Result = name  
        },  
        new WriteLine()  
        {  
            Text = new InArgument<string>((env) => "Hello, " + name.Get(env))  
        }  
    }  
};  
  
AutoResetEvent syncEvent = new AutoResetEvent(false);  
  
// Create the WorkflowApplication using the desired  
// workflow definition.  
WorkflowApplication wfApp = new WorkflowApplication(wf);  
  
// Handle the desired lifecycle events.  
wfApp.Completed = delegate(WorkflowApplicationCompletedEventArgs e)  
{  
    // Signal the host that the workflow is complete.  
    syncEvent.Set();  
};  
  
// Start the workflow.  
wfApp.Run();  
  
// Collect the user's name and resume the bookmark.  
// Bookmark resumption only occurs when the workflow  
// is idle. If a call to ResumeBookmark is made and the workflow  
// is not idle, ResumeBookmark blocks until the workflow becomes  
// idle before resuming the bookmark.  
wfApp.ResumeBookmark("UserName", Console.ReadLine());  
  
// Wait for Completed to arrive and signal that  
// the workflow is complete.  
syncEvent.WaitOne();  
```  
  
 Quando a atividade de `ReadLine` é executada, cria <xref:System.Activities.Bookmark> chamado `UserName` e espera no indexador a ser continuado. O host reúne os dados desejados e depois <xref:System.Activities.Bookmark>. Retoma de fluxo de trabalho, exibe o nome, e então usa. Observe que nenhum código de sincronização é necessário em relação ao indexador continuar. <xref:System.Activities.Bookmark> só pode ser que quando o fluxo de trabalho estiver ocioso, e se o fluxo de trabalho não estiver ocioso, a chamada para blocos de <xref:System.Activities.WorkflowApplication.ResumeBookmark%2A> até que o fluxo de trabalho se torne ocioso.  
  
## <a name="bookmark-resumption-result"></a>Resultado de ressunção do indexador  

 <xref:System.Activities.WorkflowApplication.ResumeBookmark%2A> retorna um valor de enumeração <xref:System.Activities.BookmarkResumptionResult> para indicar os resultados da solicitação de ressunção do indexador. Retornar valores possíveis são <xref:System.Activities.BookmarkResumptionResult.Success>, <xref:System.Activities.BookmarkResumptionResult.NotReady>, e <xref:System.Activities.BookmarkResumptionResult.NotFound>. Hosts e extensões podem usar esse valor para determinar como continuar.
