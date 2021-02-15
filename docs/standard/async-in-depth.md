---
title: Assincronia detalhada
description: Saiba como escrever código assíncrono associado à CPU ou à E/S é simples usando o modelo assíncrono baseado em tarefas do .NET.
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.assetid: 1e38f9d9-8f84-46ee-a15f-199aec4f2e34
ms.openlocfilehash: 7fcc41c4ea5037d643402fc722e8f16f28d560ee
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94823323"
---
# <a name="async-in-depth"></a>Assincronia detalhada

Escrever código assíncrono vinculado à CPU ou à E/S é simples usando o modelo assíncrono baseado em Tarefas do .NET. O modelo é exposto pelos tipos `Task` e `Task<T>` e pelas palavras-chave `async` e `await` no C# e no Visual Basic. (Os recursos específicos à linguagem são encontrados na seção [Consulte também](#see-also) .) Este artigo explica como usar o .NET Async e fornece informações sobre a estrutura assíncrona usada nos bastidores.

## <a name="task-and-taskt"></a>Tarefa e tarefa\<T>

Tarefas são constructos usados para implementar o que é conhecido como o [modelo de promessa de simultaneidade](https://en.wikipedia.org/wiki/Futures_and_promises).  Em resumo, elas oferecem a você uma “promessa” de que o trabalho será concluído em um momento posterior, permitindo que você coordene a promessa com uma API limpa.

- `Task` representa uma única operação que não retorna um valor.
- `Task<T>` representa uma única operação que retorna um valor do tipo `T`.

É importante pensar nas tarefas como abstrações do trabalho ocorrendo de maneira assíncrona e *não* uma abstração de threading. Por padrão, as tarefas são executadas no thread atual e delegam o trabalho para o sistema operacional, conforme apropriado. Opcionalmente, as tarefas podem ser solicitadas explicitamente para serem executadas em um thread separado por meio da API `Task.Run`.

As tarefas expõem um protocolo de API para monitoramento, aguardando e acessando o valor do resultado (no caso de `Task<T>`) de uma tarefa. A integração de linguagem, com a palavra-chave `await`, fornece uma abstração de nível mais alto para o uso de tarefas.

O uso de `await` permite que seu aplicativo ou serviço realize um trabalho útil enquanto uma tarefa estiver em execução gerando o controle para seu chamador até que a tarefa seja concluída. Seu código não precisa contar com retornos de chamada ou eventos para continuar a execução após a tarefa ter sido concluída. A integração da API da tarefa e da linguagem faz isso para você. Se você estiver usando `Task<T>`, a palavra-chave `await` "desencapsulará" adicionalmente o valor retornado quando a Tarefa for concluída.  Os detalhes de como isso funciona são explicados mais abaixo.

Você pode aprender mais sobre as tarefas e as diferentes maneiras de interagir com elas no tópico [Padrão assíncrono baseado em tarefa (TAP)](./asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).

## <a name="deeper-dive-into-tasks-for-an-io-bound-operation"></a>Aprofundamento em tarefas para uma operação vinculada à E/S

A seção a seguir descreve uma exibição de 10.000 pés do que acontece com uma chamada de E/S assíncrona típica. Vamos começar com alguns exemplos.

O primeiro exemplo chama um método assíncrono e retorna uma tarefa ativa, provavelmente ainda para ser concluída.

```csharp
public Task<string> GetHtmlAsync()
{
    // Execution is synchronous here
    var client = new HttpClient();

    return client.GetStringAsync("https://www.dotnetfoundation.org");
}
```

O segundo exemplo adiciona o uso das palavras-chave `async` e `await` para operar na tarefa.

```csharp
public async Task<string> GetFirstCharactersCountAsync(string url, int count)
{
    // Execution is synchronous here
    var client = new HttpClient();

    // Execution of GetFirstCharactersCountAsync() is yielded to the caller here
    // GetStringAsync returns a Task<string>, which is *awaited*
    var page = await client.GetStringAsync("https://www.dotnetfoundation.org");

    // Execution resumes when the client.GetStringAsync task completes,
    // becoming synchronous again.

    if (count > page.Length)
    {
        return page;
    }
    else
    {
        return page.Substring(0, count);
    }
}
```

A chamada para `GetStringAsync()` realiza a chamada por bibliotecas .NET de níveis inferiores (talvez chamando outros métodos assíncronos) até atingir uma chamada de interoperabilidade P/Invoke em uma biblioteca de rede nativa. A biblioteca nativa pode chamar subsequentemente uma chamada à API do sistema (como `write()` para um soquete no Linux). Um objeto de tarefa será criado no limite nativo/gerenciado, possivelmente usando [TaskCompletionSource](xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult(%600)). O objeto de tarefa será passado pelas camadas, possivelmente operado ou retornado diretamente, finalmente retornado ao chamador inicial.

No segundo exemplo acima, um objeto `Task<T>` será retornado de `GetStringAsync`. O uso da palavra-chave `await` faz com que o método retorne um objeto de tarefa recém-criado. O controle retorna para o chamador desse local no método `GetFirstCharactersCountAsync`. Os métodos e propriedades do objeto [Task&lt;T&gt;](xref:System.Threading.Tasks.Task%601) permitem que os chamadores monitorem o progresso da tarefa, que será concluída quando o código restante em GetFirstCharactersCountAsync for executado.

Após a chamada à API do sistema, a solicitação está no espaço de kernel, trilhando seu caminho para o subsistema de rede do sistema operacional (como `/net` no Kernel do Linux).  Aqui, o sistema operacional tratará a solicitação de rede *assincronamente*.  Os detalhes podem ser diferentes dependendo do sistema operacional usado (a chamada de driver de dispositivo pode ser agendada como um sinal enviado de volta para o runtime ou pode ser feita uma chamada de driver de dispositivo e *em seguida,* um sinal enviado de volta), mas, no fim, o runtime será informado de que a solicitação de rede está em andamento.  Neste momento, o trabalho para o driver de dispositivo estará agendado, em andamento ou já finalizado (a solicitação já está “durante a transmissão”), mas como tudo isso está ocorrendo assincronamente, o driver do dispositivo pode manipular outra coisa imediatamente.

Por exemplo, no Windows, um thread de sistema operacional faz uma chamada para o driver de dispositivo de rede e solicita que ele realize a operação de rede por meio de um IRP (Pacote de Solicitação de Interrupção), que representa a operação.  O driver de dispositivo recebe o IRP, faz a chamada para a rede, marca o IRP como "pendente" e retorna para o sistema operacional.  Como o thread do sistema operacional agora sabe que o IRP está "pendente", ele não tem mais nenhum trabalho para fazer para esse trabalho e “retorna” para que possa ser usado para realizar outro trabalho.

Quando a solicitação é atendida e os dados voltam por meio do driver de dispositivo, ele notifica a CPU sobre os novos dados recebidos por meio de uma interrupção.  Como essa interrupção é tratada variará dependendo do sistema operacional, mas, no fim, os dados serão passados pelo sistema operacional até atingirem uma chamada de interoperabilidade do sistema (por exemplo, no Linux um manipulador de interrupção agendará a metade inferior da IRQ para passar os dados pelo sistema operacional assincronamente).  Observe que isso *também* ocorre assincronamente.  O resultado é colocado na fila até que o próximo thread disponível possa executar o método assíncrono e “desencapsular” o resultado da tarefa concluída.

Durante todo esse processo, uma consideração importante é que **nenhum thread é dedicado a executar a tarefa**.  Embora o trabalho seja executado em algum contexto (ou seja, o sistema operacional tem de passar os dados para um driver de dispositivo e responder a uma interrupção), nenhum thread é dedicado a *esperar* os dados da solicitação voltarem.  Isso permite que o sistema lide com um volume muito maior de trabalho em vez de esperar que alguma chamada de E/S seja concluída.

Embora o descrito acima possa parecer muito trabalho a ser feito, quando medido em termos de tempo total, ele é minúsculo em comparação com o tempo necessário para realizar o trabalho real de E/S. Embora não seja precisa, uma linha do tempo possível para essa chamada teria esta aparência:

0-1————————————————————————————————————————————————–2-3

- O tempo gasto dos pontos `0` até `1` é tudo até um método assíncrono gerar o controle para seu chamador.
- O tempo gasto dos pontos `1` até `2` é o tempo gasto na E/S, sem custo de CPU.
- Por fim, o tempo gasto dos pontos `2` até `3` está passando o controle de volta (e potencialmente um valor) para o método assíncrono, ponto no qual está sendo executado novamente.

### <a name="what-does-this-mean-for-a-server-scenario"></a>O que isso significa para um cenário de servidor?

Esse modelo funciona bem com uma carga de trabalho de cenário de servidor típica.  Como não há nenhum thread dedicado para bloquear tarefas não concluídas, o pool de threads do servidor pode atender a um volume muito maior de solicitações da Web.

Considere dois servidores: um que executa o código assíncrono e que não faz isso.  Para esse exemplo, cada servidor tem apenas cinco threads disponíveis para solicitações de serviço.  Observe que esses números são imaginariamente pequenos e servem apenas em um contexto de demonstração.

Suponha que ambos os servidores recebem seis solicitações simultâneas. Cada solicitação executa uma operação de E/S.  O servidor *sem* o código assíncrono precisa enfileirar a sexta solicitação até que um dos cinco threads tenham concluído o trabalho vinculado à E/S e escrito uma resposta. No ponto em que a 20ª solicitação chega, o servidor pode começar a ficar lento, pois a fila está ficando muito longa.

O servidor *com* o código assíncrono em execução ainda enfileira a sexta solicitação, mas como ele usa `async` e `await`, cada um de seus threads é liberado quando o trabalho vinculado à E/S começa, em vez de quando ele é concluído.  No momento em que a 20ª solicitação chega, a fila para as solicitações recebidas é muito menor (se ela tiver algo em absoluto) e o servidor não fica lento.

Embora esse seja um exemplo inventado, ele funciona de maneira muito semelhante no mundo real.  Na verdade, você pode esperar que um servidor seja capaz de lidar com uma ordem de grandeza de mais solicitações usando `async` e `await` do que se ele estivesse dedicando um thread para cada solicitação recebida.

### <a name="what-does-this-mean-for-client-scenario"></a>O que isso significa para um cenário de cliente?

O maior ganho do uso do `async` e `await` para um aplicativo cliente é um aumento na capacidade de resposta.  Embora você possa fazer um aplicativo responsivo gerando threads manualmente, o ato de gerar um thread é uma operação cara em relação a apenas usar o `async` e `await`.  Especialmente para algo como um jogo para dispositivos móveis, afetar o thread da interface do usuário o mínimo possível no que concerne à E/S é crucial.

Mais importante, como o trabalho vinculado à E/S passa praticamente nenhum tempo na CPU, dedicar um thread de CPU inteiro para realizar quase nenhum trabalho útil seria um uso inadequado dos recursos.

Além disso, distribuir o trabalho para o thread de interface do usuário (como atualizar uma interface do usuário) é muito simples com os métodos `async` e não requer trabalho extra (como chamar um delegado thread-safe).

## <a name="deeper-dive-into-task-and-taskt-for-a-cpu-bound-operation"></a>Aprofundamento em Task e Task\<T> para uma operação vinculada à CPU

O código `async` vinculado à CPU é um pouco diferente do código `async` vinculado à E/S.  Como o trabalho é feito na CPU, não há como contornar a dedicação de um thread à computação.  O uso de `async` e `await` fornece uma maneira simples de interagir com thread em segundo plano e manter o chamador do método assíncrono responsivo.  Observe que isso não fornece nenhuma proteção para dados compartilhados.  Se você estiver usando dados compartilhados, ainda precisará aplicar uma estratégia de sincronização apropriada.

Esta é uma exibição de 10.000 pés de uma chamada assíncrona vinculada à CPU:

```csharp
public async Task<int> CalculateResult(InputData data)
{
    // This queues up the work on the threadpool.
    var expensiveResultTask = Task.Run(() => DoExpensiveCalculation(data));

    // Note that at this point, you can do some other work concurrently,
    // as CalculateResult() is still executing!

    // Execution of CalculateResult is yielded here!
    var result = await expensiveResultTask;

    return result;
}
```

`CalculateResult()` executa no thread no qual foi chamado.  Quando ele chama `Task.Run`, coloca na fila uma operação cara vinculada à CPU, `DoExpensiveCalculation()`, no pool de threads e recebe um identificador `Task<int>`.  `DoExpensiveCalculation()` é finalmente executado simultaneamente no próximo thread disponível, provavelmente em outro núcleo da CPU.  É possível fazer o trabalho simultâneo enquanto `DoExpensiveCalculation()` está ocupado em outro thread, pois o thread que chamou `CalculateResult()` ainda está em execução.

Uma vez que `await` é encontrado, a execução de `CalculateResult()` é gerada para seu chamador, permitindo que outro trabalho seja realizado com o thread atual enquanto `DoExpensiveCalculation()` está produzindo um resultado.  Ao terminar, o resultado é enfileirado para ser executado no thread principal.  No fim, o thread principal retornará para a execução de `CalculateResult()`, ponto em que ele terá o resultado de `DoExpensiveCalculation()`.

### <a name="why-does-async-help-here"></a>Por que a assincronia ajuda aqui?

`async` e `await` são a prática recomendada para gerenciar o trabalho vinculado à CPU quando você precisar de capacidade de resposta. Existem vários padrões para usar a assincronia com o trabalho vinculado à CPU. É importante observar que há um pequeno custo para usar a assincronia e não é recomendado para loops estreitos.  Cabe a você determinar como escrever seu código em torno dessa nova capacidade.

## <a name="see-also"></a>Confira também

- [Programação assíncrona em C#](../csharp/async.md)
- [Programação assíncrona com async e await (C#)](../csharp/programming-guide/concepts/async/index.md)
- [Programação assíncrona em F#](../fsharp/tutorials/asynchronous-and-concurrent-programming/async.md)
- [Programação assíncrona com Async e Await (Visual Basic)](../visual-basic/programming-guide/concepts/async/index.md)
