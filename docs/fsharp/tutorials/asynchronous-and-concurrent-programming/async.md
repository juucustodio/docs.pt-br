---
title: Programação assíncrona
description: 'Saiba como o F # fornece suporte limpo para assincronia com base em um modelo de programação de nível de linguagem derivado dos principais conceitos de programação funcional.'
ms.date: 08/15/2020
ms.openlocfilehash: 8bf8d6987187377cc1f44e77141b5d70d873f849
ms.sourcegitcommit: fcbe432482464b1639decad78cc4dc8387c6269e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366810"
---
# <a name="async-programming-in-f"></a>Programação assíncrona em F\#

A programação assíncrona é um mecanismo essencial para aplicativos modernos por vários motivos. Há dois casos de uso primários que a maioria dos desenvolvedores encontrará:

- Apresentar um processo de servidor que pode atender a um número significativo de solicitações de entrada simultâneas, minimizando os recursos do sistema ocupados enquanto o processamento da solicitação aguarda entradas de sistemas ou serviços externos a esse processo
- Manutenção de uma interface do usuário responsiva ou thread principal ao progredir o trabalho em segundo plano simultaneamente

Embora o trabalho em segundo plano geralmente envolva a utilização de vários threads, é importante considerar os conceitos de assincronia e multithreading separadamente. Na verdade, eles são preocupações separadas e um não implica o outro. Este artigo descreve os conceitos separados em mais detalhes.

## <a name="asynchrony-defined"></a>Assincronia definida

O ponto anterior – que a assincronia é independente da utilização de vários threads-vale a pena explicar um pouco mais. Há três conceitos que às vezes são relacionados, mas estritamente independentes um do outro:

- Corrente Quando vários cálculos são executados em períodos de tempo sobrepostos.
- Paralelismo Quando vários cálculos ou várias partes de uma única computação são executados exatamente ao mesmo tempo.
- Sincronismo Quando um ou mais cálculos podem ser executados separadamente do fluxo do programa principal.

Todos os três são conceitos ortogonal, mas podem ser facilmente conplanados, especialmente quando eles são usados juntos. Por exemplo, talvez seja necessário executar várias Computações assíncronas em paralelo. Essa relação não significa que o paralelismo ou a assincronia implicam um ao outro.

Se você considerar o etymology da palavra "Asynchronous", há duas partes envolvidas:

- "a", significando "não".
- "síncrono", significando "ao mesmo tempo".

Ao reunir esses dois termos, você verá que "assíncrono" significa "não ao mesmo tempo". Pronto! Não há implicação de simultaneidade ou paralelismo nessa definição. Isso também é verdade na prática.

Em termos práticos, cálculos assíncronos em F # são agendados para execução independente do fluxo do programa principal. Essa execução independente não implica em simultaneidade ou paralelismo, nem significa que uma computação sempre ocorre em segundo plano. Na verdade, as Computações assíncronas podem até mesmo executar de forma síncrona, dependendo da natureza da computação e do ambiente em que a computação está sendo executada.

O principal argumento que você deve ter é que as Computações assíncronas são independentes do fluxo do programa principal. Embora haja algumas garantias sobre quando ou como uma computação assíncrona é executada, há algumas abordagens para orquestrar e agendá-las. O restante deste artigo explora os principais conceitos de assincronia F # e como usar os tipos, funções e expressões criados no F #.

## <a name="core-concepts"></a>Conceitos fundamentais

No F #, a programação assíncrona é centralizada em cerca de três conceitos principais:

- O `Async<'T>` tipo, que representa uma computação assíncrona combinável.
- As `Async` funções de módulo, que permitem agendar trabalho assíncrono, compor Computações assíncronas e transformar resultados assíncronos.
- A `async { }` [expressão de computação](../../language-reference/computation-expressions.md), que fornece uma sintaxe conveniente para criar e controlar cálculos assíncronos.

Você pode ver esses três conceitos no exemplo a seguir:

```fsharp
open System
open System.IO

let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn $"File {fileName} has %d{bytes.Length} bytes"
    }

[<EntryPoint>]
let main argv =
    printTotalFileBytes "path-to-file.txt"
    |> Async.RunSynchronously

    Console.Read() |> ignore
    0
```

No exemplo, a `printTotalFileBytes` função é do tipo `string -> Async<unit>` . Chamar a função não executa realmente a computação assíncrona. Em vez disso, retorna um `Async<unit>` que atua como uma *especificação* do trabalho que deve ser executado de forma assíncrona. Ele chama `Async.AwaitTask` seu corpo, que converte o resultado de <xref:System.IO.File.ReadAllBytesAsync%2A> para um tipo apropriado.

Outra linha importante é a chamada para `Async.RunSynchronously` . Esse é um dos módulos assíncronos que iniciam funções que você precisará chamar se quiser realmente executar uma computação assíncrona em F #.

Essa é uma diferença fundamental com o estilo de programação C#/Visual Basic `async` . No F #, as Computações assíncronas podem ser consideradas como **tarefas frias**. Eles devem ser iniciados explicitamente para realmente executar. Isso tem algumas vantagens, pois permite combinar e sequenciar trabalho assíncrono muito mais facilmente do que em C# ou Visual Basic.

## <a name="combine-asynchronous-computations"></a>Combinar Computações assíncronas

Aqui está um exemplo que se baseia no anterior combinando cálculos:

```fsharp
open System
open System.IO

let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn $"File {fileName} has %d{bytes.Length} bytes"
    }

[<EntryPoint>]
let main argv =
    argv
    |> Seq.map printTotalFileBytes
    |> Async.Parallel
    |> Async.Ignore
    |> Async.RunSynchronously

    0
```

Como você pode ver, a `main` função tem muito mais alguns elementos. Conceitualmente, ele faz o seguinte:

1. Transforme os argumentos de linha de comando em uma sequência de `Async<unit>` cálculos com `Seq.map` .
2. Crie um `Async<'T[]>` que agenda e executa os `printTotalFileBytes` cálculos em paralelo quando ele é executado.
3. Crie um `Async<unit>` que executará a computação paralela e ignore seu resultado (que é um `unit[]` ).
4. Execute explicitamente a computação composta geral com `Async.RunSynchronously` , bloqueando até que seja concluída.

Quando esse programa é executado, `printTotalFileBytes` é executado em paralelo para cada argumento de linha de comando. Como as Computações assíncronas são executadas independentemente do fluxo do programa, não há nenhuma ordem definida na qual elas imprimem suas informações e concluam a execução. Os cálculos serão agendados em paralelo, mas a ordem de execução não será garantida.

## <a name="sequence-asynchronous-computations"></a>Computações assíncronas de sequência

Como `Async<'T>` o é uma especificação de trabalho em vez de uma tarefa já em execução, você pode executar transformações mais complexas facilmente. Aqui está um exemplo que sequencia um conjunto de Computações assíncronas para que eles executem um após o outro.

```fsharp
let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn $"File {fileName} has %d{bytes.Length} bytes"
    }

[<EntryPoint>]
let main argv =
    argv
    |> Seq.map printTotalFileBytes
    |> Async.Sequential
    |> Async.Ignore
    |> Async.RunSynchronously
    |> ignore
```

Isso agendará `printTotalFileBytes` para ser executado na ordem dos elementos em `argv` vez de agendá-los em paralelo. Como cada operação sucessiva não será agendada até a conclusão da execução da computação anterior, os cálculos serão seqüenciados de modo que não haja sobreposição na execução.

## <a name="important-async-module-functions"></a>Funções de módulo assíncrono importantes

Ao escrever código assíncrono em F #, você geralmente interage com uma estrutura que lida com o agendamento de cálculos para você. No entanto, esse não é sempre o caso, portanto, é bom entender as várias funções que podem ser usadas para agendar o trabalho assíncrono.

Como os cálculos assíncronos F # são uma _especificação_ de trabalho em vez de uma representação de trabalho que já está em execução, eles devem ser iniciados explicitamente com uma função inicial. Há muitos [métodos de início assíncrono](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpasync.html#section0) que são úteis em diferentes contextos. A seção a seguir descreve algumas das funções iniciais mais comuns.

### <a name="asyncstartchild"></a>Async. StartChild

Inicia uma computação filho em uma computação assíncrona. Isso permite que vários cálculos assíncronos sejam executados simultaneamente. A computação filho compartilha um token de cancelamento com a computação pai. Se o cálculo pai for cancelado, o cálculo filho também será cancelado.

Assinatura:

```fsharp
computation: Async<'T> * timeout: ?int -> Async<Async<'T>>
```

Quando usar:

- Quando você deseja executar várias Computações assíncronas simultaneamente em vez de uma de cada vez, mas elas não são agendadas em paralelo.
- Quando você quiser vincular o tempo de vida de uma computação filho ao de um cálculo pai.

O que deve ser observado:

- Iniciar vários cálculos com `Async.StartChild` não é o mesmo que agendá-los em paralelo. Se você quiser agendar cálculos em paralelo, use `Async.Parallel` .
- Cancelar um cálculo pai irá disparar o cancelamento de todos os cálculos filho iniciados.

### <a name="asyncstartimmediate"></a>Async. StartImmediate

Executa uma computação assíncrona, começando imediatamente no thread do sistema operacional atual. Isso será útil se você precisar atualizar algo no thread de chamada durante o cálculo. Por exemplo, se uma computação assíncrona precisar atualizar uma interface do usuário (como atualizar uma barra de progresso), `Async.StartImmediate` deverá ser usada.

Assinatura:

```fsharp
computation: Async<unit> * cancellationToken: ?CancellationToken -> unit
```

Quando usar:

- Quando você precisa atualizar algo no thread de chamada no meio de uma computação assíncrona.

O que deve ser observado:

- O código na computação assíncrona será executado em qualquer thread em que ele esteja agendado. Isso pode ser problemático se esse thread for, de alguma forma, confidencial, como um thread de interface do usuário. Nesses casos, `Async.StartImmediate` provavelmente é inadequado usar.

### <a name="asyncstartastask"></a>Async. StartAsTask

Executa uma computação no pool de threads. Retorna um <xref:System.Threading.Tasks.Task%601> que será concluído no estado correspondente depois que o cálculo for encerrado (produz o resultado, gera uma exceção ou é cancelado). Se nenhum token de cancelamento for fornecido, o token de cancelamento padrão será usado.

Assinatura:

```fsharp
computation: Async<'T> * taskCreationOptions: ?TaskCreationOptions * cancellationToken: ?CancellationToken -> Task<'T>
```

Quando usar:

- Quando você precisa chamar uma API do .NET que produz um <xref:System.Threading.Tasks.Task%601> para representar o resultado de uma computação assíncrona.

O que deve ser observado:

- Essa chamada irá alocar um `Task` objeto adicional, o que pode aumentar a sobrecarga se for usado com frequência.

### <a name="asyncparallel"></a>Async. Parallel

Agenda uma sequência de Computações assíncronas a serem executadas em paralelo, produzindo uma matriz de resultados na ordem em que foram fornecidas. O grau de paralelismo pode ser, opcionalmente, ajustado/limitado, especificando o `maxDegreeOfParallelism` parâmetro.

Assinatura:

```fsharp
computations: seq<Async<'T>> * ?maxDegreeOfParallelism: int -> Async<'T[]>
```

Quando usar:

- Se você precisar executar um conjunto de cálculos ao mesmo tempo e não tiver nenhuma dependência em sua ordem de execução.
- Se você não precisar de resultados de cálculos agendados em paralelo até que todos tenham sido concluídos.

O que deve ser observado:

- Você só pode acessar a matriz resultante de valores depois que todos os cálculos forem concluídos.
- As computações serão executadas sempre que acabarem sendo agendadas. Esse comportamento significa que você não pode contar com a ordem de sua execução.

### <a name="asyncsequential"></a>Async. Sequential

Agenda uma sequência de Computações assíncronas a serem executadas na ordem em que são passadas. O primeiro cálculo será executado e, em seguida, o próximo e assim por diante. Nenhum cálculo será executado em paralelo.

Assinatura:

```fsharp
computations: seq<Async<'T>> -> Async<'T[]>
```

Quando usar:

- Se você precisar executar vários cálculos na ordem.

O que deve ser observado:

- Você só pode acessar a matriz resultante de valores depois que todos os cálculos forem concluídos.
- As computações serão executadas na ordem em que são passadas para essa função, o que pode significar que mais tempo decorrerá antes que os resultados sejam retornados.

### <a name="asyncawaittask"></a>Async. AwaitTask

Retorna uma computação assíncrona que aguarda o determinado <xref:System.Threading.Tasks.Task%601> a ser concluído e retorna seu resultado como um `Async<'T>`

Assinatura:

```fsharp
task: Task<'T> -> Async<'T>
```

Quando usar:

- Quando você está consumindo uma API do .NET que retorna um <xref:System.Threading.Tasks.Task%601> dentro de uma computação assíncrona em F #.

O que deve ser observado:

- As exceções são encapsuladas <xref:System.AggregateException> seguindo a Convenção da biblioteca de tarefas paralelas; esse comportamento é diferente de como a F # Async geralmente faz a superfície de exceções.

### <a name="asynccatch"></a>Async. catch

Cria uma computação assíncrona que executa um determinado `Async<'T>` , retornando um `Async<Choice<'T, exn>>` . Se o determinado for `Async<'T>` concluído com êxito, um `Choice1Of2` será retornado com o valor resultante. Se uma exceção for lançada antes de ser concluída, um `Choice2of2` será retornado com a exceção gerada. Se ele for usado em uma computação assíncrona que, por sua vez, é composto por muitos cálculos, e um desses cálculos gera uma exceção, a computação que englobará o cálculo será totalmente interrompida.

Assinatura:

```fsharp
computation: Async<'T> -> Async<Choice<'T, exn>>
```

Quando usar:

- Quando você estiver executando um trabalho assíncrono que pode falhar com uma exceção e você deseja tratar essa exceção no chamador.

O que deve ser observado:

- Ao usar Computações assíncronas combinadas ou sequenciadas, a computação abrangerá completamente se um de seus cálculos "internos" gerar uma exceção.

### <a name="asyncignore"></a>Async. ignore

Cria uma computação assíncrona que executa a computação fornecida, mas descarta seu resultado.

Assinatura:

```fsharp
computation: Async<'T> -> Async<unit>
```

Quando usar:

- Quando você tem uma computação assíncrona cujo resultado não é necessário. Isso é análogo à `ignore` função de código não assíncrono.

O que deve ser observado:

- Se você precisar usar `Async.Ignore` o porque deseja usar `Async.Start` ou outra função que exija `Async<unit>` o, considere se descartar o resultado está ok. Evite descartar os resultados apenas para se ajustar a uma assinatura de tipo.

### <a name="asyncrunsynchronously"></a>Async. RunSynchronously

Executa uma computação assíncrona e aguarda seu resultado no thread de chamada. Propaga uma exceção caso a computação gere uma. Esta chamada está bloqueando.

Assinatura:

```fsharp
computation: Async<'T> * timeout: ?int * cancellationToken: ?CancellationToken -> 'T
```

Quando usar:

- Se você precisar dele, use-o apenas uma vez em um aplicativo-no ponto de entrada para um executável.
- Quando você não se importa com o desempenho e deseja executar um conjunto de outras operações assíncronas de uma vez.

O que deve ser observado:

- A chamada `Async.RunSynchronously` bloqueia o thread de chamada até que a execução seja concluída.

### <a name="asyncstart"></a>Async. Start

Inicia uma computação assíncrona que retorna `unit` no pool de threads. Não aguarda sua conclusão e/ou observa um resultado de exceção. Cálculos aninhados iniciados com `Async.Start` são iniciados independentemente do cálculo pai que os chamou; seu tempo de vida não está vinculado a nenhum cálculo pai. Se o cálculo pai for cancelado, nenhum cálculo filho será cancelado.

Assinatura:

```fsharp
computation: Async<unit> * cancellationToken: ?CancellationToken -> unit
```

Use somente quando:

- Você tem uma computação assíncrona que não produz um resultado e/ou requer o processamento de um.
- Você não precisa saber quando uma computação assíncrona é concluída.
- Você não se importa com o thread em que uma computação assíncrona é executada.
- Você não precisa estar atento ou relatar exceções resultantes da execução.

O que deve ser observado:

- Exceções geradas por computações iniciadas com `Async.Start` não são propagadas para o chamador. A pilha de chamadas será completamente desbobinada.
- Qualquer trabalho (como chamada `printfn` ) iniciado com `Async.Start` não fará com que o efeito aconteça no thread principal da execução de um programa.

## <a name="interoperate-with-net"></a>Interoperar com o .NET

Você pode estar trabalhando com uma biblioteca .NET ou codebase C# que usa programação assíncrona de estilo [Async/Await](../../../standard/async.md). Como o C# e a maioria das bibliotecas do .NET usam os <xref:System.Threading.Tasks.Task%601> <xref:System.Threading.Tasks.Task> tipos e como suas abstrações principais em vez de `Async<'T>` , você deve cruzar um limite entre essas duas abordagens para assincronia.

### <a name="how-to-work-with-net-async-and-taskt"></a>Como trabalhar com o .NET Async e `Task<T>`

Trabalhar com bibliotecas assíncronas .NET e bases de código que usam <xref:System.Threading.Tasks.Task%601> (ou seja, Computações assíncronas com valores de retorno) é simples e tem suporte interno com F #.

Você pode usar a `Async.AwaitTask` função para aguardar uma computação assíncrona do .net:

```fsharp
let getValueFromLibrary param =
    async {
        let! value = DotNetLibrary.GetValueAsync param |> Async.AwaitTask
        return value
    }
```

Você pode usar a `Async.StartAsTask` função para passar uma computação assíncrona para um chamador do .net:

```fsharp
let computationForCaller param =
    async {
        let! result = getAsyncResult param
        return result
    } |> Async.StartAsTask
```

### <a name="how-to-work-with-net-async-and-task"></a>Como trabalhar com o .NET Async e `Task`

Para trabalhar com APIs que usam <xref:System.Threading.Tasks.Task> (ou seja, Computações assíncronas do .NET que não retornam um valor), talvez seja necessário adicionar uma função adicional que converterá um `Async<'T>` para um <xref:System.Threading.Tasks.Task> :

```fsharp
module Async =
    // Async<unit> -> Task
    let startTaskFromAsyncUnit (comp: Async<unit>) =
        Async.StartAsTask comp :> Task
```

Já existe um `Async.AwaitTask` que aceita uma <xref:System.Threading.Tasks.Task> entrada as. Com isso e a função definida anteriormente `startTaskFromAsyncUnit` , você pode iniciar e esperar <xref:System.Threading.Tasks.Task> tipos de uma computação Async de F #.

## <a name="relationship-to-multi-threading"></a>Relação com multithreading

Embora o Threading seja mencionado em todo este artigo, há duas coisas importantes a serem lembradas:

1. Não há afinidade entre uma computação assíncrona e um thread, a menos que seja explicitamente iniciado no thread atual.
1. A programação assíncrona em F # não é uma abstração para multithreading.

Por exemplo, uma computação pode ser realmente executada no thread do chamador, dependendo da natureza do trabalho. Uma computação também poderia "saltar" entre threads, emprestando-os por um pequeno tempo para fazer um trabalho útil entre períodos de "espera" (como quando uma chamada de rede está em trânsito).

Embora o F # forneça algumas capacidades para iniciar uma computação assíncrona no thread atual (ou não explicitamente no thread atual), a assincronia geralmente não está associada a uma estratégia de Threading específica.

## <a name="see-also"></a>Veja também

- [O modelo de programação assíncrona F #](https://www.microsoft.com/research/publication/the-f-asynchronous-programming-model)
- [Guia assíncrono F # do Jet. com](https://medium.com/jettech/f-async-guide-eb3c8a2d180a)
- [F # para o guia de programação assíncrona de lucros e diversão](https://fsharpforfunandprofit.com/posts/concurrency-async-and-parallel/)
- [Async em C# e F #: armadilhas assíncronas em C #](http://tomasp.net/blog/csharp-async-gotchas.aspx/)
