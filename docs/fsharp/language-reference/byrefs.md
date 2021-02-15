---
title: Byrefs
description: 'Saiba mais sobre os tipos ByRef e ByRef em F #, que são usados para programação de baixo nível.'
ms.date: 11/04/2019
ms.openlocfilehash: ff2c06d8940f7341d5d8b1d942be264bfac586c5
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740309"
---
# <a name="byrefs"></a>Byrefs

O F # tem duas áreas principais de recursos que lidam com o espaço de programação de baixo nível:

* Os `byref` / `inref` / `outref` tipos, que são ponteiros gerenciados. Eles têm restrições de uso para que você não possa compilar um programa inválido em tempo de execução.
* Um `byref` struct semelhante, que é uma [estrutura](structures.md) que tem semântica semelhante e as mesmas restrições de tempo de compilação que o `byref<'T>` . Um exemplo é <xref:System.Span%601> .

## <a name="syntax"></a>Sintaxe

```fsharp
// Byref types as parameters
let f (x: byref<'T>) = ()
let g (x: inref<'T>) = ()
let h (x: outref<'T>) = ()

// Calling a function with a byref parameter
let mutable x = 3
f &x

// Declaring a byref-like struct
open System.Runtime.CompilerServices

[<Struct; IsByRefLike>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

## <a name="byref-inref-and-outref"></a>ByRef, inref e outref

Há três formas de `byref` :

* `inref<'T>`, um ponteiro gerenciado para ler o valor subjacente.
* `outref<'T>`, um ponteiro gerenciado para gravar no valor subjacente.
* `byref<'T>`, um ponteiro gerenciado para ler e gravar o valor subjacente.

Um `byref<'T>` pode ser passado onde um `inref<'T>` é esperado. Da mesma forma, um `byref<'T>` pode ser passado onde um `outref<'T>` é esperado.

## <a name="using-byrefs"></a>Usando byrefs

Para usar um `inref<'T>` , você precisa obter um valor de ponteiro com `&` :

```fsharp
open System

let f (dt: inref<DateTime>) =
    printfn $"Now: %O{dt}"

let usage =
    let dt = DateTime.Now
    f &dt // Pass a pointer to 'dt'
```

Para gravar no ponteiro usando um `outref<'T>` ou `byref<'T>` , você também deve fazer com que o valor para o qual você pegue um ponteiro `mutable` .

```fsharp
open System

let f (dt: byref<DateTime>) =
    printfn $"Now: %O{dt}"
    dt <- DateTime.Now

// Make 'dt' mutable
let mutable dt = DateTime.Now

// Now you can pass the pointer to 'dt'
f &dt
```

Se você estiver apenas escrevendo o ponteiro em vez de lê-lo, considere usar `outref<'T>` em vez de `byref<'T>` .

### <a name="inref-semantics"></a>Semântica Inref

Considere o seguinte código:

```fsharp
let f (x: inref<SomeStruct>) = x.SomeField
```

Semanticamente, isso significa o seguinte:

* O detentor do `x` ponteiro só pode usá-lo para ler o valor.
* Qualquer ponteiro adquirido para `struct` campos aninhados no `SomeStruct` recebe o tipo `inref<_>` .

O seguinte também é verdadeiro:

* Não há implicação de que outros threads ou aliases não tenham acesso de gravação `x` .
* Não há implicação `SomeStruct` de que seja imutável em virtude de `x` ser um `inref` .

No entanto, para **tipos de valor** F # imutáveis, o `this` ponteiro é inferido para ser um `inref` .

Juntas, todas essas regras significam que o detentor de um `inref` ponteiro não pode modificar o conteúdo imediato da memória que está sendo apontada.

### <a name="outref-semantics"></a>Semântica Outref

A finalidade do `outref<'T>` é indicar que o ponteiro só deve ser gravado. Inesperadamente, `outref<'T>` permite a leitura do valor subjacente, apesar do seu nome. Isso é para fins de compatibilidade. Semanticamente, `outref<'T>` não é diferente de `byref<'T>` .

### <a name="interop-with-c"></a>Interoperabilidade com C\#

O C# dá suporte às `in ref` `out ref` palavras-chave e, além de `ref` retornos. A tabela a seguir mostra como o F # interpreta o que o C# emite:

|Construção C#|Inferências de F #|
|------------|---------|
|`ref` valor de retorno|`outref<'T>`|
|`ref readonly` valor de retorno|`inref<'T>`|
|Parâmetro `in ref`|`inref<'T>`|
|Parâmetro `out ref`|`outref<'T>`|

A tabela a seguir mostra o que são emitidos em F #:

|Construção de F #|Construção emitida|
|------------|-----------------|
|Argumento `inref<'T>`|`[In]` atributo no argumento|
|`inref<'T>` exibir|`modreq` atributo no valor|
|`inref<'T>` em slot abstrato ou implementação|`modreq` no argumento ou retorno|
|Argumento `outref<'T>`|`[Out]` atributo no argumento|

### <a name="type-inference-and-overloading-rules"></a>Inferência de tipos e regras de sobrecarga

Um `inref<'T>` tipo é inferido pelo compilador F # nos seguintes casos:

1. Um parâmetro .NET ou tipo de retorno que tem um `IsReadOnly` atributo.
2. O `this` ponteiro em um tipo de struct que não tem campos mutáveis.
3. O endereço de um local de memória derivado de outro `inref<_>` ponteiro.

Quando um endereço implícito de um `inref` está sendo obtido, uma sobrecarga com um argumento do tipo `SomeType` é preferida para uma sobrecarga com um argumento do tipo `inref<SomeType>` . Por exemplo:

```fsharp
type C() =
    static member M(x: System.DateTime) = x.AddDays(1.0)
    static member M(x: inref<System.DateTime>) = x.AddDays(2.0)
    static member M2(x: System.DateTime, y: int) = x.AddDays(1.0)
    static member M2(x: inref<System.DateTime>, y: int) = x.AddDays(2.0)

let res = System.DateTime.Now
let v =  C.M(res)
let v2 =  C.M2(res, 4)
```

Em ambos os casos, as sobrecargas que levam `System.DateTime` são resolvidas, em vez das sobrecargas que levam `inref<System.DateTime>` .

## <a name="byref-like-structs"></a>Estruturas do tipo ByRef

Além do `byref` / `inref` / `outref` triodo, você pode definir suas próprias estruturas que podem aderir à `byref` semântica desejada. Isso é feito com o <xref:System.Runtime.CompilerServices.IsByRefLikeAttribute> atributo:

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsByRefLike` Não implica `Struct` . Ambos devem estar presentes no tipo.

Um `byref` struct "-Like" em F # é um tipo de valor de associação de pilha. Ele nunca é alocado no heap gerenciado. Um `byref` struct semelhante é útil para programação de alto desempenho, pois é imposta com o conjunto de verificações fortes sobre o tempo de vida e a não captura. As regras são:

* Eles podem ser usados como parâmetros de função, parâmetros de método, variáveis locais, método retorna.
* Eles não podem ser membros estáticos ou de instância de uma classe ou estrutura normal.
* Eles não podem ser capturados por nenhuma construção de fechamento ( `async` métodos ou expressões lambda).
* Eles não podem ser usados como um parâmetro genérico.

Esse último ponto é crucial para a programação em estilo de pipeline F #, como `|>` é uma função genérica que parametriza seus tipos de entrada. Essa restrição pode ser reduzida `|>` no futuro, pois está embutida e não faz nenhuma chamada para funções genéricas não embutidas em seu corpo.

Embora essas regras restrinjam fortemente o uso, elas fazem isso para atender à promessa de computação de alto desempenho de maneira segura.

## <a name="byref-returns"></a>Retornos de ByRef

O ByRef retorna de funções F # ou os membros podem ser produzidos e consumidos. Ao consumir um `byref` método que retorna, o valor é implicitamente cancelado. Por exemplo:

```fsharp
let squareAndPrint (data : byref<int>) =
    let squared = data*data    // data is implicitly dereferenced
    printfn $"%d{squared}"
```

Para retornar um valor ByRef, a variável que contém o valor deve residir mais tempo do que o escopo atual.
Além disso, para retornar ByRef, use `&value` (em que value é uma variável que permanece mais longa do que o escopo atual).

```fsharp
let mutable sum = 0
let safeSum (bytes: Span<byte>) =
    for i in 0 .. bytes.Length - 1 do
        sum <- sum + int bytes.[i]
    &sum  // sum lives longer than the scope of this function.
```

Para evitar a desreferência implícita, como passar uma referência por meio de várias chamadas encadeadas, use `&x` (onde `x` é o valor).

Você também pode atribuir diretamente a um retorno `byref` . Considere o seguinte programa (altamente imperativo):

```fsharp
type C() =
    let mutable nums = [| 1; 3; 7; 15; 31; 63; 127; 255; 511; 1023 |]

    override _.ToString() = String.Join(' ', nums)

    member _.FindLargestSmallerThan(target: int) =
        let mutable ctr = nums.Length - 1

        while ctr > 0 && nums.[ctr] >= target do ctr <- ctr - 1

        if ctr > 0 then &nums.[ctr] else &nums.[0]

[<EntryPoint>]
let main argv =
    let c = C()
    printfn $"Original sequence: %O{c}"

    let v = &c.FindLargestSmallerThan 16

    v <- v*2 // Directly assign to the byref return

    printfn $"New sequence:      %O{c}"

    0 // return an integer exit code
```

Esta é a saída:

```console
Original sequence: 1 3 7 15 31 63 127 255 511 1023
New sequence:      1 3 7 30 31 63 127 255 511 1023
```

## <a name="scoping-for-byrefs"></a>Escopo para byrefs

Um `let` valor associado não pode ter sua referência exceder o escopo no qual ele foi definido. Por exemplo, o seguinte não é permitido:

```fsharp
let test2 () =
    let x = 12
    &x // Error: 'x' exceeds its defined scope!

let test () =
    let x =
        let y = 1
        &y // Error: `y` exceeds its defined scope!
    ()
```

Isso impede que você obtenha resultados diferentes dependendo de se você compilar com otimizações ou não.
