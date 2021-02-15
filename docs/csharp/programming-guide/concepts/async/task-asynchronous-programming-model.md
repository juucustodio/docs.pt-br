---
title: O modelo de programação assíncrona de tarefa (toque) com Async e Await (C#) "
description: Saiba quando e como usar a programação assíncrona baseada em tarefas, uma abordagem simplificada para programação assíncrona em C#.
ms.date: 08/19/2020
ms.assetid: 9bcf896a-5826-4189-8c1a-3e35fa08243a
ms.openlocfilehash: 1014e38dcb3e2c4f56c8b3f3dade9bdbff3abd27
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556031"
---
# <a name="task-asynchronous-programming-model"></a>Modelo de programação assíncrona de tarefa

É possível evitar gargalos de desempenho e aprimorar a resposta geral do seu aplicativo usando a programação assíncrona. No entanto, as técnicas tradicionais para escrever aplicativos assíncronos podem ser complicadas, dificultando sua escrita, depuração e manutenção.

O [C# 5](../../../whats-new/csharp-version-history.md#c-version-50) apresentou uma programação assíncrona de abordagem simplificada que aproveita o suporte assíncrono no .NET Framework 4.5 e superior, no .NET Core e no Windows Runtime. O compilador faz o trabalho difícil que o desenvolvedor costumava fazer, e seu aplicativo mantém a estrutura lógica que se assemelha ao código síncrono. Como resultado, você obtém todas as vantagens da programação assíncrona com uma fração do esforço.

Este tópico oferece uma visão geral de quando e como usar a programação assíncrona e inclui links para tópicos de suporte que contêm detalhes e exemplos.

## <a name="async-improves-responsiveness"></a><a name="BKMK_WhentoUseAsynchrony"></a> O Async melhora a capacidade de resposta

A assincronia é essencial para atividades que são potencialmente de bloqueio, como o acesso via Web. O acesso a um recurso da Web às vezes é lento ou atrasado. Se tal atividade for bloqueada em um processo síncrono, todo o aplicativo deverá esperar. Em um processo assíncrono, o aplicativo poderá prosseguir com outro trabalho que não dependa do recurso da Web até a tarefa potencialmente causadora do bloqueio terminar.

A tabela a seguir mostra a áreas típicas onde a programação assíncrona melhora a resposta. As APIs listadas do .NET e do Windows Runtime contêm métodos que dão suporte à programação assíncrona.

| Área do aplicativo | Tipos .NET com métodos assíncronos | Tipos Windows Runtime com métodos assíncronos |
|--|--|--|
| Acesso à Web | <xref:System.Net.Http.HttpClient> | <xref:Windows.Web.Http.HttpClient?displayProperty=nameWithType> <br> <xref:Windows.Web.Syndication.SyndicationClient> |
| Trabalhando com arquivos | <xref:System.Text.Json.JsonSerializer> <br> <xref:System.IO.StreamReader> <br> <xref:System.IO.StreamWriter> <br> <xref:System.Xml.XmlReader> <br> <xref:System.Xml.XmlWriter> | <xref:Windows.Storage.StorageFile> |
| Trabalhando com imagens |  | <xref:Windows.Media.Capture.MediaCapture> <br> <xref:Windows.Graphics.Imaging.BitmapEncoder> <br> <xref:Windows.Graphics.Imaging.BitmapDecoder> |
| Programação WCF | [Operações síncronas e assíncronas](../../../../framework/wcf/synchronous-and-asynchronous-operations.md) |  |

A assincronia é especialmente importante para aplicativos que acessam o thread de interface de usuário porque todas as atividades relacionadas à interface do usuário normalmente compartilham um único thread. Se um processo for bloqueado em um aplicativo síncrono, todos serão bloqueados. Seu aplicativo para de responder, o que poderia levar você a concluir que ele falhou quando, na verdade, está apenas aguardando.

Quando você usa métodos assíncronos, o aplicativo continua a responder à interface do usuário. Você poderá redimensionar ou minimizar uma janela, por exemplo, ou fechar o aplicativo se você não desejar aguardar sua conclusão.

A abordagem baseada em assincronia adiciona o equivalente de uma transmissão automática à lista de opções disponíveis para escolha ao criar operações assíncronas. Ou seja, você obtém todos os benefícios da programação assíncrona tradicional, mas com muito menos esforço do desenvolvedor.

## <a name="async-methods-are-easy-to-write"></a><a name="BKMK_HowtoWriteanAsyncMethod"></a> Os métodos assíncronos são fáceis de escrever

As palavras-chave [async](../../../language-reference/keywords/async.md) e [await](../../../language-reference/operators/await.md) em C# são a parte central da programação assíncrona. Usando essas duas palavras-chave, você pode usar recursos no .NET Framework, no .NET Core ou no Windows Runtime para criar um método assíncrono quase tão fácil quanto criar um método síncrono. Os métodos assíncronos que você define usando a palavra-chave `async` são chamados de *métodos assíncronos*.

O exemplo a seguir mostra um método assíncrono. Quase tudo no código deve parecer familiar para você.

Você pode encontrar um exemplo completo de Windows Presentation Foundation (WPF) disponível para download da [programação assíncrona com Async e Await em C#](/samples/dotnet/samples/async-and-await-cs).

:::code language="csharp" source="snippets/access-web/Program.cs" id="ControlFlow":::

Você pode aprender várias práticas com a amostra anterior. Comece com a assinatura do método. Ele inclui o modificador `async`. O tipo de retorno é `Task<int>` (confira a seção "Tipos de retorno" para obter mais opções). O nome do método termina com `Async`. No corpo do método, `GetStringAsync` retorna uma `Task<string>`. Isso significa que, quando você executar `await` em uma tarefa, obterá uma `string` (`contents`). Antes de aguardar a tarefa, você poderá fazer um trabalho que não dependa da `string` em `GetStringAsync`.

Preste muita atenção no operador `await`. Ele suspende `GetUrlContentLengthAsync` :

- `GetUrlContentLengthAsync` não poderá continuar enquanto `getStringTask` não for concluída.
- Enquanto isso, o controle é retornado ao chamador de `GetUrlContentLengthAsync`.
- O controle será retomado aqui quando a `getStringTask` for concluída.
- Em seguida, o operador `await` recupera o resultado `string` de `getStringTask`.

A instrução de retorno especifica um resultado inteiro. Os métodos que estão aguardando `GetUrlContentLengthAsync` recuperar o valor de comprimento.

Se `GetUrlContentLengthAsync` não tiver nenhum trabalho que possa fazer entre chamar `GetStringAsync` e aguardar a conclusão, você poderá simplificar o código ao chamar e esperar na instrução única a seguir.

```csharp
string contents = await client.GetStringAsync("https://docs.microsoft.com/dotnet");
```

As características a seguir resumem o que torna o exemplo anterior um método assíncrono:

- A assinatura do método inclui um modificador `async`.
- O nome de um método assíncrono, por convenção, termina com um sufixo "Async".
- O tipo de retorno é um dos seguintes tipos:

  - <xref:System.Threading.Tasks.Task%601> se o método possui uma instrução de retorno em que o operando tem o tipo `TResult`.
  - <xref:System.Threading.Tasks.Task> se o método não possui instrução de retorno alguma ou se ele possui uma instrução de retorno sem operando.
  - `void` se você estiver escrevendo um manipulador de eventos assíncronos.
  - Qualquer outro tipo que tenha um método `GetAwaiter` (começando com o C# 7.0).

  Para obter mais informações, consulte a seção [tipos de retorno e parâmetros](#BKMK_ReturnTypesandParameters) .

- O método geralmente inclui, pelo menos, uma expressão `await`, que marca um ponto em que o método não poderá continuar enquanto a operação assíncrona aguardada não for concluída. Enquanto isso, o método é suspenso e o controle retorna para o chamador do método. A próxima seção deste tópico ilustra o que acontece no ponto de suspensão.

Em métodos assíncronos, você usa as palavras-chave e os tipos fornecidos para indicar o que deseja fazer, e o compilador faz o resto, inclusive acompanhar o que deve acontecer quando o controle retorna a um ponto de espera em um método suspenso. Alguns processos de rotina, como loops e a manipulação de exceções, podem ser difíceis de manipular em um código assíncrono tradicional. Em um método assíncrono, você escreve esses elementos da mesma forma que faria em uma solução síncrona, e o problema é resolvido.

Para obter mais informações sobre assincronia em versões anteriores do .NET Framework, consulte [tpl e programação assíncrona de .NET Framework tradicional](../../../../standard/parallel-programming/tpl-and-traditional-async-programming.md).

## <a name="what-happens-in-an-async-method"></a><a name="BKMK_WhatHappensUnderstandinganAsyncMethod"></a> O que acontece em um método assíncrono

O mais importante que você deve compreender na programação assíncrona é a forma como o fluxo de controle avança de um método para outro. O diagrama a seguir pode ser usado para conduzi-lo pelo processo:

:::image type="content" source="media/task-asynchronous-programming-model/navigation-trace-async-program.png" alt-text="Navegação de rastreamento do fluxo de controle assíncrono" lightbox="media/task-asynchronous-programming-model/navigation-trace-async-program.png":::

Os números no diagrama correspondem às etapas a seguir, iniciadas quando um método de chamada chama o método Async.

1. Um método de chamada chama e aguarda o `GetUrlContentLengthAsync` método Async.

1. `GetUrlContentLengthAsync` cria uma instância de <xref:System.Net.Http.HttpClient> e chama o método assíncrono <xref:System.Net.Http.HttpClient.GetStringAsync%2A> para baixar o conteúdo de um site como uma cadeia de caracteres.

1. Algo acontece em `GetStringAsync` que suspende o andamento. Talvez ele deva aguardar o download de um site ou alguma outra atividade causadora de bloqueio. Para evitar o bloqueio de recursos, `GetStringAsync` transfere o controle para seu chamador, `GetUrlContentLengthAsync`.

     `GetStringAsync` retorna um <xref:System.Threading.Tasks.Task%601>, em que `TResult` é uma cadeia de caracteres, e `GetUrlContentLengthAsync` atribui a tarefa à variável `getStringTask`. A tarefa representa o processo contínuo para a chamada a `GetStringAsync`, com um compromisso de produzir um valor de cadeia de caracteres real quando o trabalho estiver concluído.

1. Como o `getStringTask` ainda não foi esperado, `GetUrlContentLengthAsync` pode continuar com outro trabalho que não depende do resultado final de `GetStringAsync`. O trabalho é representado por uma chamada ao método síncrono `DoIndependentWork`.

1. `DoIndependentWork` é um método síncrono que faz seu trabalho e retorna ao seu chamador.

1. `GetUrlContentLengthAsync` está sem trabalho que ele possa executar sem um resultado de `getStringTask`. Em seguida, `GetUrlContentLengthAsync` deseja calcular e retornar o comprimento da cadeia de caracteres baixada, mas o método não poderá calcular o valor enquanto o método tiver a cadeia de caracteres.

    Portanto, `GetUrlContentLengthAsync` usa um operador await para suspender seu andamento e para transferir o controle para o método que chamou `GetUrlContentLengthAsync`. `GetUrlContentLengthAsync` retorna um `Task<int>` ao chamador. A tarefa representa uma promessa de produzir um resultado inteiro que é o comprimento da cadeia de caracteres baixada.

    > [!NOTE]
    > Se `GetStringAsync` (e, portanto, `getStringTask`) for concluído antes que `GetUrlContentLengthAsync` o aguarde, o controle permanecerá em `GetUrlContentLengthAsync`. A despesa de suspender e de retornar para `GetUrlContentLengthAsync` seria desperdiçada se o processo assíncrono `getStringTask` já tiver sido concluído e `GetUrlContentLengthAsync` não tiver que esperar pelo resultado final.

    Dentro do método de chamada, o padrão de processamento continua. O chamador pode fazer outro trabalho que não dependa do resultado de `GetUrlContentLengthAsync` antes de aguardar o resultado, ou o chamador pode aguardar imediatamente. O método de chamada está aguardando `GetUrlContentLengthAsync` e `GetUrlContentLengthAsync` está aguardando `GetStringAsync` .

1. `GetStringAsync` completa e produz um resultado de cadeia de caracteres. O resultado da cadeia de caracteres não é retornado pela chamada para `GetStringAsync` da maneira que você poderia esperar. (Lembre-se que o método já retornou uma tarefa na etapa 3.) Em vez disso, o resultado da cadeia de caracteres é armazenado na tarefa que representa a conclusão do método, `getStringTask`. O operador await recupera o resultado de `getStringTask`. A instrução de atribuição atribui o resultado retornado a `contents`.

1. Quando `GetUrlContentLengthAsync` tem o resultado da cadeia de caracteres, o método pode calcular o comprimento da cadeia de caracteres. Em seguida, o trabalho de `GetUrlContentLengthAsync` também é concluído e o manipulador de eventos de espera poderá retomar. No exemplo completo no final do tópico, é possível confirmar que o manipulador de eventos recuperou e imprimiu o valor do comprimento do resultado.
Se você não tiver experiência em programação assíncrona, considere por um minuto a diferença entre o comportamento síncrono e o assíncrono. Um método síncrono retorna quando seu trabalho é concluído (etapa 5), mas um método assíncrono retorna um valor de tarefa quando seu trabalho está suspenso (etapas 3 e 6). Quando o método assíncrono eventualmente concluir seu trabalho, a tarefa será marcada como concluída e o resultado, se houver, será armazenado na tarefa.

## <a name="api-async-methods"></a><a name="BKMK_APIAsyncMethods"></a> Métodos assíncronos de API

Você pode estar curioso para saber onde encontrar métodos como `GetStringAsync` que oferecem suporte à programação assíncrona. .NET Framework 4,5 ou superior e o .NET Core contêm muitos membros que funcionam com o `async` e o `await` . Você pode reconhecê-los pelo sufixo "Async" que é anexado ao nome do membro e por seu tipo de retorno de <xref:System.Threading.Tasks.Task> ou <xref:System.Threading.Tasks.Task%601> . Por exemplo, a classe `System.IO.Stream` contém métodos como <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.ReadAsync%2A> e <xref:System.IO.Stream.WriteAsync%2A>, juntamente com os métodos síncronos <xref:System.IO.Stream.CopyTo%2A>, <xref:System.IO.Stream.Read%2A> e <xref:System.IO.Stream.Write%2A>.

O Windows Runtime também contém vários métodos que você pode usar com `async` e `await` em aplicativos do Windows. Para obter mais informações, veja [Threading e programação assíncrona](/windows/uwp/threading-async/) para o desenvolvimento da UWP e [Programação assíncrona (aplicativos da Windows Store)](/previous-versions/windows/apps/hh464924(v=win.10)) e [Início Rápido: chamando APIs assíncronas em C# ou Visual Basic](/previous-versions/windows/apps/hh452713(v=win.10)) se você usa versões anteriores do Windows Runtime.

## <a name="threads"></a><a name="BKMK_Threads"></a> Threads

Os métodos assíncronos destinam-se a ser operações não causadoras de bloqueios. Uma `await` expressão em um método assíncrono não bloqueia o thread atual enquanto a tarefa esperada está em execução. Em vez disso, a expressão anterior assina o restante do método como uma continuação e retorna o controle para o chamador do método assíncrono.

As palavras-chave `async` e `await` não fazem com que threads adicionais sejam criados. Os métodos assíncronos não exigem multithreading, pois um método assíncrono não executa em seu próprio thread. O método é executado no contexto de sincronização atual e usa tempo no thread somente quando o método está ativo. É possível usar <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> para mover o trabalho de CPU associado a um thread em segundo plano, mas um thread em segundo plano não ajuda com um processo que está apenas aguardando que os resultados tornem-se disponíveis.

A abordagem baseada em async para a programação assíncrona é preferível às abordagens existentes em quase todos os casos. Essa abordagem é especialmente mais eficiente do que a classe <xref:System.ComponentModel.BackgroundWorker> para operações de entrada e saída, porque o código é mais simples e você não precisa se proteger contra condições de corrida. Em combinação com o <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> método, a programação assíncrona é melhor do que <xref:System.ComponentModel.BackgroundWorker> para operações associadas à CPU porque a programação assíncrona separa os detalhes de coordenação da execução do código do trabalho que `Task.Run` transfere para o pool de threads.

## <a name="async-and-await"></a><a name="BKMK_AsyncandAwait"></a> Async e Await

Se você especificar que um método é assíncrono usando um modificador [async](../../../language-reference/keywords/async.md), você habilitará os dois recursos a seguir.

- O método assíncrono marcado pode usar [await](../../../language-reference/operators/await.md) para designar pontos de suspensão. O operador `await` informa ao compilador que o método assíncrono não poderá continuar além daquele ponto até que o processo assíncrono aguardado seja concluído. Enquanto isso, o controle retorna para o chamador do método assíncrono.

     A suspensão de um método assíncrono em uma `await` expressão não constitui uma saída do método e os `finally` blocos não são executados.

- O método assíncrono marcado pode ele próprio ser aguardado por métodos que o chamam.

Um método assíncrono normalmente contém uma ou mais ocorrências de um `await` operador, mas a ausência de `await` expressões não causa um erro de compilador. Se um método assíncrono não usar um `await` operador para marcar um ponto de suspensão, o método será executado como um método síncrono, apesar do `async` modificador. O compilador emite um aviso para esses métodos.

`async` e `await` são palavras-chave contextuais. Para obter mais informações e exemplos, consulte os seguintes tópicos:

- [async](../../../language-reference/keywords/async.md)
- [await](../../../language-reference/operators/await.md)

## <a name="return-types-and-parameters"></a><a name="BKMK_ReturnTypesandParameters"></a> Tipos de retorno e parâmetros

Um método assíncrono normalmente retorna <xref:System.Threading.Tasks.Task> ou <xref:System.Threading.Tasks.Task%601>. Dentro de um método assíncrono, um operador `await` é aplicado a uma tarefa que é retornada de uma chamada para outro método assíncrono.

Você especifica <xref:System.Threading.Tasks.Task%601> como o tipo de retorno se o método contiver uma [`return`](../../../language-reference/keywords/return.md) instrução que especifica um operando do tipo `TResult` .

Você usará <xref:System.Threading.Tasks.Task> como o tipo de retorno se o método não tiver nenhuma instrução return ou se tiver uma instrução return que não retorna um operando.

Começando com C# 7.0, também será possível especificar qualquer outro tipo de retorno, desde que o tipo inclua um método `GetAwaiter`. <xref:System.Threading.Tasks.ValueTask%601> é um exemplo de tal tipo. Ele está disponível no pacote NuGet [System.Threading.Tasks.Extension](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/).

O exemplo a seguir mostra como você declara e chama um método que retorna um <xref:System.Threading.Tasks.Task%601> ou um <xref:System.Threading.Tasks.Task> :

```csharp
async Task<int> GetTaskOfTResultAsync()
{
    int hours = 0;
    await Task.Delay(0);

    return hours;
}


Task<int> returnedTaskTResult = GetTaskOfTResultAsync();
int intResult = await returnedTaskTResult;
// Single line
// int intResult = await GetTaskOfTResultAsync();

async Task GetTaskAsync()
{
    await Task.Delay(0);
    // No return statement needed
}

Task returnedTask = GetTaskAsync();
await returnedTask;
// Single line
await GetTaskAsync();
```

Cada tarefa retornada representa um trabalho em andamento. Uma tarefa encapsula informações sobre o estado do processo assíncrono e, consequentemente, o resultado final do processo ou a exceção que o processo apresenta quando não é bem-sucedido.

Um método assíncrono também pode ter um tipo de retorno `void`. Esse tipo de retorno é usado principalmente para definir manipuladores de eventos, onde o tipo de retorno `void` é necessário. Os manipuladores de eventos assíncronos geralmente servem como o ponto de partida para programas assíncronos.

Um método assíncrono que tem um `void` tipo de retorno não pode ser aguardado, e o chamador de um método de retorno nulo não pode capturar nenhuma exceção que o método gera.

O método não pode declarar nenhum parâmetro [in](../../../language-reference/keywords/in-parameter-modifier.md), [ref](../../../language-reference/keywords/ref.md) ou [out](../../../language-reference/keywords/out-parameter-modifier.md), mas pode chamar métodos com tais parâmetros. Da mesma forma, um método assíncrono não pode retornar um valor por referência, embora possa chamar métodos com valores retornados ref.

Para obter mais informações e exemplos, consulte [tipos de retorno assíncrono (C#)](async-return-types.md). Para obter mais informações sobre como capturar exceções nos métodos assíncronos, consulte [try-catch](../../../language-reference/keywords/try-catch.md).

As APIs assíncronas na programação do Windows Runtime têm um dos seguintes tipos de retorno, que são semelhantes às tarefas:

- <xref:Windows.Foundation.IAsyncOperation%601>, que corresponde a <xref:System.Threading.Tasks.Task%601>
- <xref:Windows.Foundation.IAsyncAction>, que corresponde a <xref:System.Threading.Tasks.Task>
- <xref:Windows.Foundation.IAsyncActionWithProgress%601>
- <xref:Windows.Foundation.IAsyncOperationWithProgress%602>

## <a name="naming-convention"></a><a name="BKMK_NamingConvention"></a> Convenção de nomenclatura

Por convenção, os métodos que retornam tipos comumente awaitable (por exemplo,,,, `Task` `Task<T>` `ValueTask` `ValueTask<T>` ) devem ter nomes que terminem com "Async". Os métodos que iniciam uma operação assíncrona, mas não retornam um tipo aguardável não devem ter nomes que terminam com "Async", mas podem começar com "Begin", "Start" ou algum outro verbo que indique que esse método não retorna nem gera o resultado da operação.

É possível ignorar a convenção quando um evento, uma classe base ou um contrato de interface sugere um nome diferente. Por exemplo, você não deve renomear manipuladores de eventos comuns, como `OnButtonClick` .

## <a name="related-topics-and-samples-visual-studio"></a><a name="BKMK_RelatedTopics"></a> Tópicos e exemplos relacionados (Visual Studio)

| Título | Descrição | Amostra |
|--|--|--|
| [Como fazer várias solicitações da Web em paralelo usando Async e Await (C#)](./index.md) | Demonstra como iniciar várias tarefas ao mesmo tempo. | [Exemplo de assincronia: fazer várias solicitações da Web paralelamente](https://code.msdn.microsoft.com/Async-Make-Multiple-Web-49adb82e) |
| [Tipos de retorno assíncrono (C#)](async-return-types.md) | Ilustra os tipos que os métodos assíncronos podem retornar e explica quando cada tipo é apropriado. |  |
| Cancelar tarefas com um token de cancelamento como um mecanismo de sinalização. | Mostra como adicionar a seguinte funcionalidade à sua solução assíncrona:<br><br> - [Cancelar uma lista de tarefas (C#)](cancel-an-async-task-or-a-list-of-tasks.md)<br>- [Cancelar tarefas após um período de tempo (C#)](cancel-async-tasks-after-a-period-of-time.md)<br>- [Processar tarefa assíncrona como concluída (C#)](start-multiple-async-tasks-and-process-them-as-they-complete.md) |  |
| [Usando Async para acesso a arquivos (C#)](using-async-for-file-access.md) | Lista e demonstra as vantagens de usar async e await para acessar arquivos. |  |
| [Padrão assíncrono baseado em tarefa (toque)](../../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) | Descreve um padrão assíncrono, o padrão é baseado nos <xref:System.Threading.Tasks.Task> tipos e <xref:System.Threading.Tasks.Task%601> . |  |
| [Vídeos sobre assincronia no Channel 9](https://channel9.msdn.com/search?term=async%20&type=All#pubDate=year&ch9Search&lang-en=en) | Fornece links para uma variedade de vídeos sobre programação assíncrona. |  |

## <a name="see-also"></a>Confira também

- [async](../../../language-reference/keywords/async.md)
- [await](../../../language-reference/operators/await.md)
- [Programação assíncrona](../../../async.md)
- [Visão geral da assincronia](../../../../standard/async.md)
