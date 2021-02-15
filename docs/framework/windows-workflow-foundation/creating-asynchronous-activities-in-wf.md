---
title: Criando atividades assíncrono em WF
description: Saiba como criar atividades assíncronas personalizadas usando o AsyncCodeActivity, que permite que as atividades derivadas implementem a lógica de execução assíncrona.
ms.date: 03/30/2017
ms.assetid: 497e81ed-5eef-460c-ba55-fae73c05824f
ms.openlocfilehash: a03fbde1ff27084cc36dffc3a1912220d9bbca7e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242078"
---
# <a name="creating-asynchronous-activities-in-wf"></a>Criando atividades assíncrono em WF

fornece<xref:System.Activities.AsyncCodeActivity> autores de atividade de uma classe base para usar que permite atividades derivados para implementar a lógica assíncrona de execução. Isso é útil para as atividades personalizados que devem realizar o trabalho assíncrona sem armazenar o segmento de agendador de fluxo de trabalho e bloquear quaisquer atividades que podem ser capaz executar paralelamente. Este tópico fornece uma visão geral sobre como criar atividades assíncronos personalizados usando <xref:System.Activities.AsyncCodeActivity>.  
  
## <a name="using-asynccodeactivity"></a>Usando AsyncCodeActivity  

 fornece<xref:System.Activities?displayProperty=nameWithType> autores personalizados de atividade com classes base diferentes para diferentes requisitos de criação da atividade. Cada um leva um semântico específico e fornece um autor de fluxo de trabalho (e o runtime da atividade) um contrato correspondente. Uma atividade com base <xref:System.Activities.AsyncCodeActivity> é uma atividade que executem o trabalho de forma assíncrona relativo ao segmento de agendador e o cujo a lógica de execução é expressa no código gerenciado. Como resultado de ir assíncrona, <xref:System.Activities.AsyncCodeActivity> pode induzir um ponto ocioso durante a execução. Devido a natureza temporária de trabalho assíncrona, <xref:System.Activities.AsyncCodeActivity> sempre cria um nenhum persistir o pacote para a duração de execução da atividade. Isso impede o runtime de fluxo de trabalho persistir a instância de fluxo de trabalho no meio de trabalho assíncrono, e também impede que a instância de fluxo de trabalho descarregar quando o código assíncrono executar.  
  
### <a name="asynccodeactivity-methods"></a>Métodos de AsyncCodeActivity  

 As atividades que derivam de <xref:System.Activities.AsyncCodeActivity> podem criar a lógica assíncrona de execução substituindo o <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e métodos de <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> com o código personalizado. Quando chamados em runtime, esses métodos são passados <xref:System.Activities.AsyncCodeActivityContext>. <xref:System.Activities.AsyncCodeActivityContext>permite que o autor da atividade forneça o estado compartilhado <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> /  <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> na Propriedade do contexto <xref:System.Activities.AsyncCodeActivityContext.UserState%2A> . No exemplo a seguir, uma atividade de `GenerateRandom` gerencia um número aleatório de forma assíncrona.  
  
 [!code-csharp[CFX_ActivityExample#8](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#8)]  
  
 A atividade do exemplo anterior deriva de <xref:System.Activities.AsyncCodeActivity%601>, e tem-se `OutArgument<int>` alto chamado `Result`. O valor retornado pelo método de `GetRandom` é extraído e retornado pela sobrescrita do <xref:System.Activities.AsyncCodeActivity%601.EndExecute%2A> , e esse valor é definido como o valor de `Result` . As atividades assíncronas que não retornam um resultado devem derivar de <xref:System.Activities.AsyncCodeActivity>. No exemplo a seguir, uma atividade de `DisplayRandom` é definida que deriva de <xref:System.Activities.AsyncCodeActivity>. Esta atividade é como a atividade de `GetRandom` mas em vez de retornar um resultado exibe uma mensagem para o console.  
  
 [!code-csharp[CFX_ActivityExample#11](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#11)]  
  
 Observe que porque não há nenhum valor de retorno, `DisplayRandom` usa <xref:System.Action> em vez de <xref:System.Func%602> para chamar seu representante, e o representante não retorna nenhum valor.  
  
 <xref:System.Activities.AsyncCodeActivity> também fornece uma substituição de <xref:System.Activities.AsyncCodeActivity.Cancel%2A> . Quando o <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> substituições são necessárias, <xref:System.Activities.AsyncCodeActivity.Cancel%2A> é opcional, e pode ser substituído para que a atividade pode limpar seu estado assíncrono excelente quando está sendo cancelada ou aborted. Se limpeza é possível e `AsyncCodeActivity.ExecutingActivityInstance.IsCancellationRequested` é `true`, a atividade deve chamar <xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A>. Todas as exceções geradas do método são fatais à instância do fluxo de trabalho.  
  
 [!code-csharp[CFX_ActivityExample#10](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#10)]  
  
### <a name="invoking-asynchronous-methods-on-a-class"></a>Chamando métodos assíncronos em uma classe  

 Muitas das classes no .NET Framework fornecem funcionalidade assíncrona, e essa funcionalidade pode ser invocada de forma assíncrona usando uma <xref:System.Activities.AsyncCodeActivity> atividade baseada. No exemplo a seguir, é criada uma atividade que cria de forma assíncrona um arquivo usando a <xref:System.IO.FileStream> classe.  
  
 [!code-csharp[CFX_ActivityExample#12](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#12)]  
  
### <a name="sharing-state-between-the-beginexecute-and-endexecute-methods"></a>Compartilhando o estado entre o BeginExecute e métodos de EndExecute  

 No exemplo anterior, o objeto de <xref:System.IO.FileStream> que foi criado em <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> foi acessado em <xref:System.Activities.AsyncCodeActivity.EndExecute%2A>. Isso é possível porque a variável de `file` foi passado a propriedade de <xref:System.Activities.AsyncCodeActivityContext.UserState%2A?displayProperty=nameWithType> no <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>. Este é o método correto para compartilhar o estado entre o <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e o <xref:System.Activities.AsyncCodeActivity.EndExecute%2A>. Está incorreto usar um variável de membro na classe derivada`FileWriter` (neste caso) para compartilhar o estado entre o <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e o <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> porque o objeto de atividade pode ser referenciado por várias instâncias de atividade. Tentar usar um variável de membro para compartilhar o estado pode resultar em valores de um <xref:System.Activities.ActivityInstance> que substitui ou que consome valores de outro <xref:System.Activities.ActivityInstance>.  
  
### <a name="accessing-argument-values"></a>Acessando valores de argumento  

 O ambiente de <xref:System.Activities.AsyncCodeActivity> consiste nos argumentos definidos na atividade. Esses argumentos podem ser acessados a partir das <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> / <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> substituições usando o <xref:System.Activities.AsyncCodeActivityContext> parâmetro. Os argumentos não podem ser acessados no delegado, mas os valores de argumento ou todos os outros dados desejados podem ser passados para o representante que usa seus parâmetros. No exemplo a seguir, uma atividade de geração aleatória é definida que obtenha o limite superior inclusive de seu argumento de `Max` . O valor do argumento é passado para o código assíncrona quando o representante é chamado.  
  
 [!code-csharp[CFX_ActivityExample#9](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#9)]  
  
### <a name="scheduling-actions-or-child-activities-using-asynccodeactivity"></a>Ações de programação ou atividades filhos usando AsyncCodeActivity  

 <xref:System.Activities.AsyncCodeActivity> derivado atividades personalizados fornece um método para fazer o trabalho de forma assíncrona com relação ao segmento de fluxo de trabalho, mas não fornece a capacidade de agendar atividades filho ou ações. No entanto, o comportamento assíncrono pode ser inserido com programação de atividades filho através de composição. Uma atividade assíncrona pode ser criada, e redigir em com <xref:System.Activities.Activity> ou <xref:System.Activities.NativeActivity> derivado a atividade para fornecer o comportamento assíncrono e a programação de atividades filho ou de ações. Por exemplo, uma atividade pode ser criada que é derivado de <xref:System.Activities.Activity>, e tem como sua implementação <xref:System.Activities.Statements.Sequence> que contém a atividade assíncrono também as outras atividades que implementam a lógica de atividade. Para obter mais exemplos de como compor atividades usando <xref:System.Activities.Activity> <xref:System.Activities.NativeActivity> o e o, consulte [como criar uma atividade](how-to-create-an-activity.md) e [Opções de criação de atividades](activity-authoring-options-in-wf.md).  
  
## <a name="see-also"></a>Confira também

- <xref:System.Action>
- <xref:System.Func%602>
