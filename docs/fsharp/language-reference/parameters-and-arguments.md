---
title: Parâmetros e argumentos
description: 'Saiba mais sobre o suporte à linguagem F # para definir parâmetros e passar argumentos para funções, métodos e propriedades.'
ms.date: 08/15/2020
ms.openlocfilehash: 3c391ca37a1cf3bd150316943e5b06efa532b317
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740283"
---
# <a name="parameters-and-arguments"></a>Parâmetros e argumentos

Este tópico descreve o suporte a idiomas para definir parâmetros e passar argumentos para funções, métodos e propriedades. Ele inclui informações sobre como passar por referência e como definir e usar métodos que podem usar um número variável de argumentos.

## <a name="parameters-and-arguments"></a>Parâmetros e argumentos

O *parâmetro* Term é usado para descrever os nomes de valores que devem ser fornecidos. O *argumento* de termo é usado para os valores fornecidos para cada parâmetro.

Os parâmetros podem ser especificados no formulário tupla ou na forma curried, ou em alguma combinação dos dois. Você pode passar argumentos usando um nome de parâmetro explícito. Parâmetros de métodos podem ser especificados como opcionais e recebem um valor padrão.

## <a name="parameter-patterns"></a>Padrões de parâmetro

Os parâmetros fornecidos a funções e métodos são, em geral, padrões separados por espaços. Isso significa que, em princípio, qualquer um dos padrões descritos em [expressões de correspondência](match-expressions.md) pode ser usado em uma lista de parâmetros para uma função ou um membro.

Normalmente, os métodos usam a forma de tupla de argumentos de passagem. Isso alcança um resultado mais claro da perspectiva de outras linguagens .NET porque o formulário de tupla corresponde à maneira como os argumentos são passados em métodos .NET.

O formulário na forma curried é usado com mais frequência com funções criadas usando `let` associações.

O pseudocódigo a seguir mostra exemplos de argumentos de tupla e na forma curried.

```fsharp
// Tuple form.
member this.SomeMethod(param1, param2) = ...
// Curried form.
let function1 param1 param2 = ...
```

Formulários combinados são possíveis quando alguns argumentos estão em tuplas e outros não são.

```fsharp
let function2 param1 (param2a, param2b) param3 = ...
```

Outros padrões também podem ser usados em listas de parâmetros, mas se o padrão de parâmetro não corresponder a todas as entradas possíveis, poderá haver uma correspondência incompleta no tempo de execução. A exceção `MatchFailureException` é gerada quando o valor de um argumento não corresponde aos padrões especificados na lista de parâmetros. O compilador emite um aviso quando um padrão de parâmetro permite correspondências incompletas. Pelo menos um outro padrão é normalmente útil para listas de parâmetros, e esse é o padrão curinga. Você usa o padrão curinga em uma lista de parâmetros quando simplesmente deseja ignorar todos os argumentos fornecidos. O código a seguir ilustra o uso do padrão curinga em uma lista de argumentos.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3801.fs)]

O padrão curinga pode ser útil sempre que você não precisar dos argumentos passados, como no ponto de entrada principal para um programa, quando você não estiver interessado nos argumentos de linha de comando que normalmente são fornecidos como uma matriz de cadeia de caracteres, como no código a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3802.fs)]

Outros padrões que às vezes são usados em argumentos são o `as` padrão e os padrões de identificador associados a uniões discriminadas e padrões ativos. Você pode usar o padrão de união discriminada de caso único da seguinte maneira.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3803.fs)]

A saída é a seguinte.

```console
Data begins at 0 and ends at 4 in string Et tu, Brute?
Et tu
```

Os padrões ativos podem ser úteis como parâmetros, por exemplo, ao transformar um argumento em um formato desejado, como no exemplo a seguir:

```fsharp
type Point = { x : float; y : float }

let (| Polar |) { x = x; y = y} =
    ( sqrt (x*x + y*y), System.Math.Atan (y/ x) )

let radius (Polar(r, _)) = r
let angle (Polar(_, theta)) = theta
```

Você pode usar o `as` padrão para armazenar um valor correspondente como um valor local, como é mostrado na linha de código a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3805.fs)]

Outro padrão usado ocasionalmente é uma função que deixa o último argumento sem nome, fornecendo, como o corpo da função, uma expressão lambda que executa imediatamente uma correspondência de padrão no argumento implícito. Um exemplo disso é a linha de código a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3804.fs)]

Esse código define uma função que usa uma lista genérica e retorna `true` se a lista estiver vazia e, `false` caso contrário,. O uso dessas técnicas pode tornar o código mais difícil de ler.

Ocasionalmente, os padrões que envolvem correspondências incompletas são úteis, por exemplo, se você souber que as listas em seu programa têm apenas três elementos, você pode usar um padrão como o seguinte em uma lista de parâmetros.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3806.fs)]

O uso de padrões que têm correspondências incompletas é melhor reservado para rápida criação de protótipos e outros usos temporários. O compilador emitirá um aviso para esse código. Tais padrões não podem abranger o caso geral de todas as entradas possíveis e, portanto, não são adequadas para APIs de componente.

## <a name="named-arguments"></a>Argumentos nomeados

Argumentos para métodos podem ser especificados por posição em uma lista de argumentos separados por vírgulas ou podem ser passados para um método explicitamente fornecendo o nome, seguido por um sinal de igual e o valor a ser passado. Se especificado fornecendo o nome, eles podem aparecer em uma ordem diferente da usada na declaração.

Os argumentos nomeados podem tornar o código mais legível e mais adaptável para determinados tipos de alterações na API, como uma reordenação de parâmetros de método.

Os argumentos nomeados são permitidos somente para métodos, não para `let` funções associadas, valores de função ou expressões lambda.

O exemplo de código a seguir demonstra o uso de argumentos nomeados.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3807.fs)]

Em uma chamada para um construtor de classe, você pode definir os valores das propriedades da classe usando uma sintaxe semelhante à dos argumentos nomeados. O exemplo a seguir mostra essa sintaxe.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

Para obter mais informações, consulte [construtores (F #)](members/constructors.md).

## <a name="optional-parameters"></a>Parâmetros Opcionais

Você pode especificar um parâmetro opcional para um método usando um ponto de interrogação na frente do nome do parâmetro. Os parâmetros opcionais são interpretados como o tipo de opção F #, de modo que você pode consultá-los de forma regular que os tipos de opção são consultados, usando uma `match` expressão com `Some` and `None` . Parâmetros opcionais são permitidos somente em membros, não em funções criadas usando `let` associações.

Você pode passar valores opcionais existentes para o método pelo nome do parâmetro, como `?arg=None` ou `?arg=Some(3)` ou `?arg=arg` . Isso pode ser útil ao criar um método que passe argumentos opcionais para outro método.

Você também pode usar uma função `defaultArg` , que define um valor padrão de um argumento opcional. A `defaultArg` função usa o parâmetro opcional como o primeiro argumento e o valor padrão como o segundo.

O exemplo a seguir ilustra o uso de parâmetros opcionais.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3808.fs)]

A saída é a seguinte.

```console
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
Baud Rate: 300 Duplex: Half Parity: true
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 9600 Duplex: Full Parity: false
Baud Rate: 4800 Duplex: Half Parity: false
```

Para fins de C# e Visual Basic interoperabilidade, você pode usar os atributos `[<Optional; DefaultParameterValue<(...)>]` em F #, para que os chamadores vejam um argumento como opcional. Isso é equivalente a definir o argumento como opcional em C# como no `MyMethod(int i = 3)` .

```fsharp
open System
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue("Hello world")>] message) =
        printfn $"{message}"
```

Você também pode especificar um novo objeto como um valor de parâmetro padrão. Por exemplo, o `Foo` membro poderia ter um opcional `CancellationToken` como entrada, em vez disso:

```fsharp
open System.Threading
open System.Runtime.InteropServices
type C =
    static member Foo([<Optional; DefaultParameterValue(CancellationToken())>] ct: CancellationToken) =
        printfn $"{ct}"
```

O valor fornecido como argumento para `DefaultParameterValue` deve corresponder ao tipo do parâmetro. Por exemplo, o seguinte não é permitido:

```fsharp
type C =
    static member Wrong([<Optional; DefaultParameterValue("string")>] i:int) = ()
```

Nesse caso, o compilador gera um aviso e ignorará os dois atributos completamente. Observe que o valor padrão `null` precisa ser anotado por tipo, como caso contrário, o compilador infere o tipo errado, ou seja, `[<Optional; DefaultParameterValue(null:obj)>] o:obj` .

## <a name="passing-by-reference"></a>Passando por referência

A passagem de um valor F # por referência envolve [byrefs](byrefs.md), que são tipos de ponteiros gerenciados. As diretrizes para o tipo a ser usado são as seguintes:

- Use `inref<'T>` se você precisar apenas ler o ponteiro.
- Use `outref<'T>` se você precisar apenas gravar no ponteiro.
- Use `byref<'T>` se você precisar ler e gravar no ponteiro.

```fsharp
let example1 (x: inref<int>) = printfn $"It's %d{x}"

let example2 (x: outref<int>) = x <- x + 1

let example3 (x: byref<int>) =
    printfn $"It's %d{x}"
    x <- x + 1

let test () =
    // No need to make it mutable, since it's read-only
    let x = 1
    example1 &x

    // Needs to be mutable, since we write to it
    let mutable y = 2
    example2 &y
    example3 &y // Now 'y' is 3
```

Como o parâmetro é um ponteiro e o valor é mutável, todas as alterações no valor são mantidas após a execução da função.

Você pode usar uma tupla como um valor de retorno para armazenar quaisquer `out` parâmetros em métodos de biblioteca do .net. Como alternativa, você pode tratar o `out` parâmetro como um `byref` parâmetro. O exemplo de código a seguir ilustra as duas maneiras.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-1/snippet3810.fs)]

## <a name="parameter-arrays"></a>Matrizes de parâmetros

Ocasionalmente, é necessário definir uma função que usa um número arbitrário de parâmetros de tipo heterogêneo. Não seria prático criar todos os métodos sobrecarregados possíveis para considerar todos os tipos que poderiam ser usados. As implementações do .NET fornecem suporte para esses métodos por meio do recurso de matriz de parâmetros. Um método que usa uma matriz de parâmetros em sua assinatura pode ser fornecido com um número arbitrário de parâmetros. Os parâmetros são colocados em uma matriz. O tipo dos elementos da matriz determina os tipos de parâmetro que podem ser passados para a função. Se você definir a matriz de parâmetros com `System.Object` como o tipo de elemento, o código do cliente poderá passar valores de qualquer tipo.

Em F #, as matrizes de parâmetros só podem ser definidas em métodos. Eles não podem ser usados em funções ou funções autônomas definidas em módulos.

Você define uma matriz de parâmetros usando o `ParamArray` atributo. O `ParamArray` atributo só pode ser aplicado ao último parâmetro.

O código a seguir ilustra a chamada de um método .NET que usa uma matriz de parâmetros e a definição de um tipo em F # que tem um método que usa uma matriz de parâmetros.

[!code-fsharp[Main](~/samples/snippets/fsharp/parameters-and-arguments-2/snippet3811.fs)]

Quando executado em um projeto, a saída do código anterior é a seguinte:

```console
a 1 10 Hello world 1 True
"a"
1
10.0
"Hello world"
1u
true
```

## <a name="see-also"></a>Confira também

- [Membros](./members/index.md)
