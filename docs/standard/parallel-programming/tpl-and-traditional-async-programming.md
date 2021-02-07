---
description: 'Saiba mais sobre: TPL e programação assíncrona .NET tradicional'
title: TPL e Programação Assíncrona do .NET Tradicional
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, with other asynchronous models
ms.assetid: e7b31170-a156-433f-9f26-b1fc7cd1776f
ms.openlocfilehash: 91eb5aad3202a016422dade7a01177ba5a82be83
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99731468"
---
# <a name="tpl-and-traditional-net-asynchronous-programming"></a>TPL e programação assíncrona .NET tradicional

O .NET fornece os dois padrões padrão a seguir para executar operações assíncronas vinculadas a e/s e de computação:  
  
- O APM (modelo de programação assíncrona), no qual as operações assíncronas são representadas por um par de métodos Begin/End. Por exemplo: <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> e <xref:System.IO.Stream.EndRead%2A?displayProperty=nameWithType>.  
  
- O padrão assíncrono baseado em evento (EAP), no qual as operações assíncronas são representadas por um par de método/evento que são nomeados `<OperationName>Async` e `<OperationName>Completed` . Por exemplo: <xref:System.Net.WebClient.DownloadStringAsync%2A?displayProperty=nameWithType> e <xref:System.Net.WebClient.DownloadStringCompleted?displayProperty=nameWithType>.
  
A Biblioteca paralela de tarefas (TPL) pode ser usada de várias maneiras, junto com qualquer um dos padrões assíncronos. Você pode expor operações de APM e EAP como `Task` objetos para consumidores de biblioteca ou pode expor os padrões de APM, mas usar `Task` objetos para implementá-los internamente. Em ambos os cenários, usando `Task` objetos, você pode simplificar o código e aproveitar as seguintes funcionalidades úteis:  
  
- Registrar chamadas de retorno, sob a forma de continuação de tarefas, a qualquer momento após a tarefa ter começado.  
  
- Coordenar várias operações executadas em resposta a um `Begin_` método usando os <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> métodos e <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> , ou os <xref:System.Threading.Tasks.Task.WaitAll%2A> métodos e <xref:System.Threading.Tasks.Task.WaitAny%2A> .  
  
- Encapsular operações assíncronas associadas a e/s no mesmo `Task` objeto.  
  
- Monitore o status do `Task` objeto.  
  
- Marshaling do status de uma operação para um `Task` objeto usando <xref:System.Threading.Tasks.TaskCompletionSource%601> .  
  
## <a name="wrap-apm-operations-in-a-task"></a>Encapsular operações de APM em uma tarefa  

 As <xref:System.Threading.Tasks.TaskFactory?displayProperty=nameWithType> classes e <xref:System.Threading.Tasks.TaskFactory%601?displayProperty=nameWithType> fornecem várias sobrecargas dos <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A?displayProperty=nameWithType> <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> métodos e que permitem encapsular um par de método Begin/End de APM em uma <xref:System.Threading.Tasks.Task> instância ou <xref:System.Threading.Tasks.Task%601> . As várias sobrecargas acomodam qualquer par de método Begin/End que tenha de zero a três parâmetros de entrada.  
  
 Para pares que têm `End` métodos que retornam um valor (a `Function` em Visual Basic), use os métodos em <xref:System.Threading.Tasks.TaskFactory%601> que criar um <xref:System.Threading.Tasks.Task%601> . Para `End` métodos que retornam void (a `Sub` em Visual Basic), use os métodos em <xref:System.Threading.Tasks.TaskFactory> que criar um <xref:System.Threading.Tasks.Task> .  
  
 Para os poucos casos em que o método `Begin` possui mais de três parâmetros ou contém parâmetros `ref` ou `out`, são fornecidas sobrecargas `FromAsync` adicionais que encapsulam apenas o método `End`.  
  
 O exemplo a seguir mostra a assinatura para a sobrecarga `FromAsync` que corresponde aos métodos <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> e <xref:System.IO.FileStream.EndRead%2A?displayProperty=nameWithType>.
  
 [!code-csharp[FromAsync#01](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#01)]
 [!code-vb[FromAsync#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#01)]  
  
Essa sobrecarga leva três parâmetros de entrada, da seguinte forma. O primeiro parâmetro é um delegado <xref:System.Func%606> que corresponde à assinatura do método <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType>. O segundo parâmetro é um delegado <xref:System.Func%602> que leva um <xref:System.IAsyncResult> e retorna um `TResult`. Como <xref:System.IO.FileStream.EndRead%2A> retorna um inteiro, o compilador infere o tipo de `TResult` como <xref:System.Int32> e o tipo da tarefa como <xref:System.Threading.Tasks.Task>. Os últimos quatro parâmetros são idênticos aos do método <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType>:  
  
- O buffer no qual armazenar os dados do arquivo.  
  
- O deslocamento no buffer no qual começar a gravar dados.  
  
- O volume máximo de dados a serem lidos a partir do arquivo.  
  
- Um objeto opcional que armazena dados de estado definidos pelo usuário para passar para o retorno de chamada.  
  
### <a name="use-continuewith-for-the-callback-functionality"></a>Usar ContinueWith para a funcionalidade de retorno de chamada

 Se você precisar acessar os dados no arquivo, em vez de apenas o número de bytes, o método <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> não é suficiente. Em vez disso, use <xref:System.Threading.Tasks.Task>, cuja propriedade `Result` contém os dados do arquivo. Você pode fazer isso adicionando uma continuação à tarefa original. A continuação executa o trabalho que normalmente seria executado pelo delegado <xref:System.AsyncCallback>. É invocada quando o antecedente é concluído e o buffer de dados foi preenchido. (O objeto <xref:System.IO.FileStream> deve ser fechado antes de retornar).  
  
 O exemplo a seguir mostra como retornar um <xref:System.Threading.Tasks.Task> que encapsula o `BeginRead` / `EndRead` par da <xref:System.IO.FileStream> classe.  
  
 [!code-csharp[FromAsync#03](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#03)]
 [!code-vb[FromAsync#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#03)]  
  
 O método pode ser chamado, da seguinte maneira.  
  
 [!code-csharp[FromAsync#04](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#04)]
 [!code-vb[FromAsync#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#04)]  
  
### <a name="provide-custom-state-data"></a>Fornecer dados de estado personalizados

 Em operações <xref:System.IAsyncResult> típicas, se o seu delegado <xref:System.AsyncCallback> precisar de alguns dados de estado personalizados, você deve passá-lo através do último parâmetro no método `Begin`, para que os dados possam ser empacotados no objeto <xref:System.IAsyncResult>, que é eventualmente passado para o método de retorno de chamada. Normalmente, isso não é necessário quando os métodos `FromAsync` são usados. Se os dados personalizados forem conhecidos pela continuação, ele poderão ser capturados diretamente no delegado de continuação. O exemplo a seguir se assemelha ao exemplo anterior, mas em vez de examinar a propriedade `Result` do antecedente, a continuação examina os dados de estado personalizados que são diretamente acessíveis ao delegado de usuário da continuação.  
  
 [!code-csharp[FromAsync#05](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#05)]
 [!code-vb[FromAsync#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#05)]  
  
### <a name="synchronize-multiple-fromasync-tasks"></a>Sincronizar várias tarefas do FromAsync

 Os métodos estáticos <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> e <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> proporcionam maior flexibilidade quando usados em conjunto com os métodos `FromAsync`. O exemplo a seguir mostra como iniciar várias operações de E/S assíncronas e aguarda que todas elas sejam concluídas antes de executar a continuação.  
  
 [!code-csharp[FromAsync#06](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#06)]
 [!code-vb[FromAsync#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#06)]  
  
### <a name="fromasync-tasks-for-only-the-end-method"></a>Tarefas FromAsync apenas para o método End

 Para esses poucos casos em que o `Begin` método requer mais de três parâmetros de entrada ou `ref` tem `out` parâmetros ou, você pode usar as `FromAsync` sobrecargas, por exemplo, <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%600%7D%29?displayProperty=nameWithType> , que representam apenas o `End` método. Esses métodos também podem ser usados em qualquer cenário no qual você passa um <xref:System.IAsyncResult> e deseja encapsulá-lo em uma tarefa.  
  
 [!code-csharp[FromAsync#07](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#07)]
 [!code-vb[FromAsync#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#07)]  
  
### <a name="start-and-cancel-fromasync-tasks"></a>Iniciar e cancelar tarefas de FromAsync

 A tarefa retornada por um `FromAsync` método tem um status de `WaitingForActivation` e será iniciada pelo sistema em algum momento depois que a tarefa for criada. Se você tentar chamar Start em tal tarefa, uma exceção será gerada.  
  
 Não é possível cancelar uma `FromAsync` tarefa, pois as APIs do .NET subjacentes atualmente não dão suporte ao cancelamento em andamento de e/s de arquivo ou de rede. Você pode adicionar funcionalidades de cancelamento a um método que encapsula uma chamada `FromAsync`, mas você só pode responder ao cancelamento antes que `FromAsync` seja chamado ou depois de concluído (por exemplo, em uma tarefa de continuação).  
  
 Algumas classes que dão suporte ao EAP, por exemplo, <xref:System.Net.WebClient>, dão suporte ao cancelamento e você pode integrar essa funcionalidade de cancelamento nativa usando tokens de cancelamento.  
  
## <a name="expose-complex-eap-operations-as-tasks"></a>Expor operações EAP complexas como tarefas

 O TPL não fornece nenhum método especificamente projetado para encapsular uma operação assíncrona baseada em eventos da mesma maneira que a família de métodos `FromAsync` envolve o padrão <xref:System.IAsyncResult>. No entanto, o TPL fornece a classe <xref:System.Threading.Tasks.TaskCompletionSource%601?displayProperty=nameWithType>, que pode ser usada para representar qualquer conjunto arbitrário de operações como <xref:System.Threading.Tasks.Task%601>. As operações podem ser síncronas ou assíncronas, e podem estar ligadas à E/S ou computação, ou ambos.  
  
 O exemplo a seguir mostra como usar um <xref:System.Threading.Tasks.TaskCompletionSource%601> para expor um conjunto de operações <xref:System.Net.WebClient> assíncronas ao código do cliente como um <xref:System.Threading.Tasks.Task%601> básico. O método permite que você insira uma série de URLs da Web e um termo ou nome para pesquisar e, em seguida, retorna o número de vezes que o termo de pesquisa ocorre em cada site.  
  
 [!code-csharp[FromAsync#10](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/snippet10.cs#10)]
 [!code-vb[FromAsync#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/snippet10.vb#10)]  
  
 Para um exemplo mais completo, que inclui a manipulação de exceções adicionais e mostra como chamar o método do código do cliente, confira [Como encapsular padrões de EAP em uma tarefa](how-to-wrap-eap-patterns-in-a-task.md).  
  
 Lembre-se de que qualquer tarefa criada por um <xref:System.Threading.Tasks.TaskCompletionSource%601> será iniciada por ela `TaskCompletionSource` e, portanto, o código do usuário não deve chamar o `Start` método nessa tarefa.  
  
## <a name="implement-the-apm-pattern-by-using-tasks"></a>Implementar o padrão APM usando tarefas

 Em alguns cenários, pode ser desejável expor diretamente o <xref:System.IAsyncResult> padrão usando pares de método Begin/End em uma API. Por exemplo, talvez você queira manter a consistência com APIs existentes, ou você pode ter ferramentas automatizadas que exigem esse padrão. Nesses casos, você pode usar `Task` objetos para simplificar como o padrão APM é implementado internamente.  
  
 O exemplo a seguir mostra como usar tarefas para implementar um par de métodos de início/término do APM para um método associado de computação de longa execução.  
  
 [!code-csharp[FromAsync#09](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#09)]
 [!code-vb[FromAsync#09](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#09)]  
  
## <a name="use-the-streamextensions-sample-code"></a>Usar o código de exemplo StreamExtensions

 O arquivo *StreamExtensions.cs* , no repositório de [extras .net Standard extensões paralelas](/samples/dotnet/samples/parallel-programming-extensions-extras-cs/) , contém várias implementações de referência que usam `Task` objetos para e/s de rede e de arquivo assíncrono.
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de tarefas paralelas (TPL)](task-parallel-library-tpl.md)
