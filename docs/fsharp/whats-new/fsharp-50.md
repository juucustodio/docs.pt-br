---
title: 'O que há de novo no guia F # 5,0-F #'
description: 'Obtenha uma visão geral dos novos recursos disponíveis em F # 5,0.'
ms.date: 11/06/2020
ms.openlocfilehash: 9b138e4801a3e599db650990acd53c0f956b78b8
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190722"
---
# <a name="whats-new-in-f-50"></a>O que há de novo no F # 5,0

O f # 5,0 adiciona várias melhorias à linguagem F # e à F# Interativo. Ele é lançado com o **.NET 5**.

Você pode baixar o SDK do .NET mais recente na [página de downloads do .net](https://dotnet.microsoft.com/download).

## <a name="get-started"></a>Introdução

O F # 5,0 está disponível em todas as distribuições do .NET Core e ferramentas do Visual Studio. Para obter mais informações, consulte Introdução ao [F #](../get-started/index.md) para saber mais.

## <a name="package-references-in-f-scripts"></a>Referências de pacote em scripts F #

O F # 5 traz suporte para referências de pacote em scripts F # com `#r "nuget:..."` sintaxe. Por exemplo, considere a seguinte referência de pacote:

```fsharp
#r "nuget: Newtonsoft.Json"

open Newtonsoft.Json

let o = {| X = 2; Y = "Hello" |}

printfn $"{JsonConvert.SerializeObject o}"
```

Você também pode fornecer uma versão explícita após o nome do pacote como este:

```fsharp
#r "nuget: Newtonsoft.Json,11.0.1"
```

As referências de pacote dão suporte a pacotes com dependências nativas, como ML.NET.

As referências de pacote também dão suporte a pacotes com requisitos especiais sobre como referenciar s dependentes `.dll` . Por exemplo, o pacote [FParsec](https://www.nuget.org/packages/FParsec/) usado para exigir que os usuários verifiquem manualmente se seu dependente foi referenciado `FParsecCS.dll` primeiro antes `FParsec.dll` de foi referenciado no F# interativo. Isso não é mais necessário e você pode fazer referência ao pacote da seguinte maneira:

```fsharp
#r "nuget: FParsec"

open FParsec

let test p str =
    match run p str with
    | Success(result, _, _)   -> printfn $"Success: {result}"
    | Failure(errorMsg, _, _) -> printfn $"Failure: {errorMsg}"

test pfloat "1.234"
```

Esse recurso implementa a [ferramenta F # do RFC FST-1027](https://github.com/fsharp/fslang-design/blob/master/tooling/FST-1027-fsi-references.md). Para obter mais informações sobre referências de pacote, consulte o tutorial de [F# interativo](../tools/fsharp-interactive/index.md) .

## <a name="string-interpolation"></a>Interpolação de cadeia de caracteres

As cadeias de caracteres interpoladas em F # são bastante semelhantes às cadeias de caracteres interpoladas em C# ou JavaScript, pois permitem escrever código em "buracos" dentro de um literal de cadeia de caracteres. Este é um exemplo básico:

```fsharp
let name = "Phillip"
let age = 29
printfn $"Name: {name}, Age: {age}"

printfn $"I think {3.0 + 0.14} is close to {System.Math.PI}!"
```

No entanto, as cadeias de caracteres interpoladas em F # também permitem interpolações com tipo, assim como a `sprintf` função, para impor que uma expressão dentro de um contexto interpolado esteja em conformidade com um tipo específico. Ele usa os mesmos especificadores de formato.

```fsharp
let name = "Phillip"
let age = 29

printfn $"Name: %s{name}, Age: %d{age}"

// Error: type mismatch
printfn $"Name: %s{age}, Age: %d{name}"
```

No exemplo de interpolação de tipo anterior, o `%s` requer que a interpolação seja do Type `string` , enquanto o `%d` requer que a interpolação seja um `integer` .

Além disso, qualquer expressão F # arbitrária (ou expressões) pode ser colocada no lado de um contexto de interpolação. É possível, até mesmo, escrever uma expressão mais complicada, da seguinte forma:

```fsharp
let str =
    $"""The result of squaring each odd item in {[1..10]} is:
{
    let square x = x * x
    let isOdd x = x % 2 <> 0
    let oddSquares xs =
        xs
        |> List.filter isOdd
        |> List.map square
    oddSquares [1..10]
}
"""
```

Embora não seja recomendável fazer isso muito na prática.

Esse recurso implementa o [F # RFC FS-1001](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1001-StringInterpolation.md).

## <a name="support-for-nameof"></a>Suporte para nameof

O F # 5 dá suporte ao `nameof` operador, que resolve o símbolo que está sendo usado e produz seu nome na fonte F #. Isso é útil em vários cenários, como registro em log e protege o registro em log contra alterações no código-fonte.

```fsharp
let months =
    [
        "January"; "February"; "March"; "April";
        "May"; "June"; "July"; "August"; "September";
        "October"; "November"; "December"
    ]

let lookupMonth month =
    if (month > 12 || month < 1) then
        invalidArg (nameof month) (sprintf "Value passed in was %d." month)

    months.[month-1]

printfn $"{lookupMonth 12}"
printfn $"{lookupMonth 1}"
printfn $"{lookupMonth 13}"
```

A última linha gerará uma exceção e "month" será mostrada na mensagem de erro.

Você pode usar um nome de quase todas as construções em F #:

```fsharp
module M =
    let f x = nameof x

printfn $"{M.f 12}"
printfn $"{nameof M}"
printfn $"{nameof M.f}"
```

Três adições finais são alterações na forma como os operadores funcionam: a adição do `nameof<'type-parameter>` formulário para parâmetros de tipo genérico e a capacidade de usar `nameof` como um padrão em uma expressão de correspondência de padrões.

Usar um nome de um operador fornece sua cadeia de caracteres de origem. Se você precisar do formulário compilado, use o nome compilado de um operador:

```fsharp
nameof(+) // "+"
nameof op_Addition // "op_Addition"
```

A obtenção do nome de um parâmetro de tipo requer uma sintaxe ligeiramente diferente:

```fsharp
type C<'TType> =
    member _.TypeName = nameof<'TType>
```

Isso é semelhante aos `typeof<'T>` operadores e `typedefof<'T>` .

O F # 5 também adiciona suporte a um `nameof` padrão que pode ser usado em `match` expressões:

```fsharp
[<Struct; IsByRefLike>]
type RecordedEvent = { EventType: string; Data: ReadOnlySpan<byte> }

type MyEvent =
    | AData of int
    | BData of string

let deserialize (e: RecordedEvent) : MyEvent =
    match e.EventType with
    | nameof AData -> AData (JsonSerializer.Deserialize<int> e.Data)
    | nameof BData -> BData (JsonSerializer.Deserialize<string> e.Data)
    | t -> failwithf "Invalid EventType: %s" t
```

O código anterior usa ' nameof ' em vez do literal de cadeia de caracteres na expressão Match.

Esse recurso implementa o [F # RFC FS-1003](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1003-nameof-operator.md).

## <a name="open-type-declarations"></a>Abrir declarações de tipo

O F # 5 também adiciona suporte para declarações de tipo aberto. Uma declaração de tipo aberto é como abrir uma classe estática em C#, exceto com alguma sintaxe diferente e um comportamento ligeiramente diferente para se ajustar à semântica de F #.

Com declarações de tipo aberto, você pode `open` qualquer tipo para expor conteúdo estático dentro dele. Além disso, você pode `open` exibir as uniões e registros definidos em F # para expor seu conteúdo. Por exemplo, isso pode ser útil se você tiver uma União definida em um módulo e desejar acessar seus casos, mas não quiser abrir o módulo inteiro.

```fsharp
open type System.Math

let x = Min(1.0, 2.0)

module M =
    type DU = A | B | C

    let someOtherFunction x = x + 1

// Open only the type inside the module
open type M.DU

printfn $"{A}"
```

Diferentemente do C#, quando você `open type` em dois tipos que expõem um membro com o mesmo nome, o membro do último tipo que está sendo `open` Ed sombreia o outro nome. Isso é consistente com a semântica F # em relação à sombra que já existe.

Esse recurso implementa o [F # RFC FS-1068](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1068-open-type-declaration.md).

## <a name="consistent-slicing-behavior-for-built-in-data-types"></a>Comportamento de divisão consistente para tipos de dados internos

Comportamento para dividir os tipos de dados internos `FSharp.Core` (matriz, lista, Cadeia de caracteres, matriz 2D, matriz 3D, matriz 4D) usado para não ser consistente antes do F # 5. Um comportamento de caso de borda lançou uma exceção e algumas delas. No F # 5, todos os tipos internos agora retornam fatias vazias para fatias que são impossíveis de gerar:

```fsharp
let l = [ 1..10 ]
let a = [| 1..10 |]
let s = "hello!"

// Before: would return empty list
// F# 5: same
let emptyList = l.[-2..(-1)]

// Before: would throw exception
// F# 5: returns empty array
let emptyArray = a.[-2..(-1)]

// Before: would throw exception
// F# 5: returns empty string
let emptyString = s.[-2..(-1)]
```

Esse recurso implementa o [F # RFC FS-1077](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-tolerant-slicing.md).

## <a name="fixed-index-slices-for-3d-and-4d-arrays-in-fsharpcore"></a>Fatias de índice fixo para matrizes 3D e 4D no FSharp. Core

O F # 5,0 oferece suporte para fatiar com um índice fixo nos tipos de matriz 3D e 4D internos.

Para ilustrar isso, considere a seguinte matriz 3D:

*z = 0*
| x\y   | 0 | 1 |
|-------|---|---|
| **0** | 0 | 1 |
| **1** | 2 | 3 |

*z = 1*
| x\y   | 0 | 1 |
|-------|---|---|
| **0** | 4 | 5 |
| **1** | 6 | 7 |

E se você quisesse extrair a fatia `[| 4; 5 |]` da matriz? Agora isso é muito simples!

```fsharp
// First, create a 3D array to slice

let dim = 2
let m = Array3D.zeroCreate<int> dim dim dim

let mutable count = 0

for z in 0..dim-1 do
    for y in 0..dim-1 do
        for x in 0..dim-1 do
            m.[x,y,z] <- count
            count <- count + 1

// Now let's get the [4;5] slice!
m.[*, 0, 1]
```

Esse recurso implementa o [F # RFC FS-1077b](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1077-3d-4d-fixed-index-slicing.md).

## <a name="f-quotations-improvements"></a>Melhorias de Cotações de F #

As [Cotações de código](../language-reference/code-quotations.md) F # agora têm a capacidade de reter informações de restrição de tipo. Considere o seguinte exemplo:

```fsharp
open FSharp.Linq.RuntimeHelpers

let eval q = LeafExpressionConverter.EvaluateQuotation q

let inline negate x = -x
// val inline negate: x: ^a ->  ^a when  ^a : (static member ( ~- ) :  ^a ->  ^a)

<@ negate 1.0 @>  |> eval
```

A restrição gerada pela `inline` função é mantida na cotação de código. O `negate` formulário quotated da função agora pode ser avaliado.

Esse recurso implementa o [F # RFC FS-1071](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1071-witness-passing-quotations.md).

## <a name="applicative-computation-expressions"></a>Expressões de computação Applicative

As [expressões de computação (CES)](../language-reference/computation-expressions.md) são usadas hoje para modelar "computações contextuais", ou em uma terminologia mais funcional com programação amigável, computações monadics.

O F # 5 apresenta Applicative CEs, que oferece um modelo computacional diferente. O Applicative CEs permite cálculos mais eficientes, desde que cada computação seja independente e seus resultados sejam acumulados no final. Quando as computações são independentes umas das outras, elas também são trivialmente paralelizáveis, permitindo que os autores de CE escrevam bibliotecas mais eficientes. No entanto, esse benefício apresenta uma restrição: as computações que dependem de valores calculados anteriormente não são permitidas.

O exemplo a seguir mostra um Applicative CE básico para o `Result` tipo.

```fsharp
// First, define a 'zip' function
module Result =
    let zip x1 x2 =
        match x1,x2 with
        | Ok x1res, Ok x2res -> Ok (x1res, x2res)
        | Error e, _ -> Error e
        | _, Error e -> Error e

// Next, define a builder with 'MergeSources' and 'BindReturn'
type ResultBuilder() =
    member _.MergeSources(t1: Result<'T,'U>, t2: Result<'T1,'U>) = Result.zip t1 t2
    member _.BindReturn(x: Result<'T,'U>, f) = Result.map f x

let result = ResultBuilder()

let run r1 r2 r3 =
    // And here is our applicative!
    let res1: Result<int, string> =
        result {
            let! a = r1
            and! b = r2
            and! c = r3
            return a + b - c
        }

    match res1 with
    | Ok x -> printfn $"{nameof res1} is: %d{x}"
    | Error e -> printfn $"{nameof res1} is: {e}"

let printApplicatives () =
    let r1 = Ok 2
    let r2 = Ok 3 // Error "fail!"
    let r3 = Ok 4

    run r1 r2 r3
    run r1 (Error "failure!") r3
```

Se você é um autor de biblioteca que expõe CEs em sua biblioteca hoje, há algumas considerações adicionais que você precisará conhecer.

Esse recurso implementa o [F # RFC FS-1063](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1063-support-letbang-andbang-for-applicative-functors.md).

## <a name="interfaces-can-be-implemented-at-different-generic-instantiations"></a>As interfaces podem ser implementadas em instanciações genéricas diferentes

Agora você pode implementar a mesma interface em instanciações genéricas diferentes:

```fsharp
type IA<'T> =
    abstract member Get : unit -> 'T

type MyClass() =
    interface IA<int> with
        member x.Get() = 1
    interface IA<string> with
        member x.Get() = "hello"

let mc = MyClass()
let iaInt = mc :> IA<int>
let iaString = mc :> IA<string>

iaInt.Get() // 1
iaString.Get() // "hello"
```

Esse recurso implementa o [F # RFC FS-1031](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1031-Allow%20implementing%20the%20same%20interface%20at%20different%20generic%20instantiations%20in%20the%20same%20type.md).

## <a name="default-interface-member-consumption"></a>Consumo de membro de interface padrão

O F # 5 permite que você consuma [interfaces com implementações padrão](../../csharp/tutorials/default-interface-methods-versions.md).

Considere uma interface definida em C# da seguinte maneira:

```csharp
using System;

namespace CSharp
{
    public interface MyDimasd
    {
        public int Z => 0;
    }
}
```

Você pode consumi-lo em F # por meio de qualquer um dos meios padrão de implementação de uma interface:

```fsharp
open CSharp

// You can implement the interface via a class
type MyType() =
    member _.M() = ()

    interface MyDim

let md = MyType() :> MyDim
printfn $"DIM from C#: %d{md.Z}"

// You can also implement it via an object expression
let md' = { new MyDim }
printfn $"DIM from C# but via Object Expression: %d{md'.Z}"
```

Isso permite que você aproveite com segurança os componentes do código C# e do .NET escritos em C# moderno quando eles esperam que os usuários possam consumir uma implementação padrão.

Esse recurso implementa o [F # RFC FS-1074](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1074-default-interface-member-consumption.md).

## <a name="simplified-interop-with-nullable-value-types"></a>Interoperabilidade simplificada com tipos de valor anulável

Os [tipos anuláveis (de valor)](/dotnet/api/system.nullable-1) (chamados de tipos anuláveis historicamente) têm o suporte de F #, mas interagir com eles tem sido tradicionalmente um problema, pois você teria que construir um `Nullable` `Nullable<SomeType>` wrapper ou cada vez que quisesse passar um valor. Agora, o compilador converterá implicitamente um tipo de valor em um `Nullable<ThatValueType>` se o tipo de destino corresponder. O código a seguir agora é possível:

```fsharp
#r "nuget: Microsoft.Data.Analysis"

open Microsoft.Data.Analysis

let dateTimes = PrimitiveDataFrameColumn<DateTime>("DateTimes")

// The following line used to fail to compile
dateTimes.Append(DateTime.Parse("2019/01/01"))

// The previous line is now equivalent to this line
dateTimes.Append(Nullable<DateTime>(DateTime.Parse("2019/01/01")))
```

Esse recurso implementa o [F # RFC FS-1075](https://github.com/fsharp/fslang-design/blob/master/FSharp-5.0/FS-1075-nullable-interop.md).

## <a name="preview-reverse-indexes"></a>Visualização: índices inversos

O F # 5 também apresenta uma visualização para permitir índices inversos. A sintaxe é `^idx`. Veja como você pode um valor de elemento 1 do final de uma lista:

```fsharp
let xs = [1..10]

// Get element 1 from the end:
xs.[^1]

// From the end slices

let lastTwoOldStyle = xs.[(xs.Length-2)..]

let lastTwoNewStyle = xs.[^1..]

lastTwoOldStyle = lastTwoNewStyle // true
```

Você também pode definir índices inversos para seus próprios tipos. Para fazer isso, você precisará implementar o seguinte método:

```fsharp
GetReverseIndex: dimension: int -> offset: int
```

Aqui está um exemplo para o `Span<'T>` tipo:

```fsharp
open System

type Span<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

    member sp.GetReverseIndex(_, offset: int) =
        sp.Length - offset

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn $"{arr}"

let run () =
    let sp = [| 1; 2; 3; 4; 5 |].AsSpan()

    // Pre-# 5.0 slicing on a Span<'T>
    printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
    printSpan sp.[..3] // [|1; 2; 3|]
    printSpan sp.[1..3] // |2; 3|]

    // Same slices, but only using from-the-end index
    printSpan sp.[..^0] // [|1; 2; 3; 4; 5|]
    printSpan sp.[..^2] // [|1; 2; 3|]
    printSpan sp.[^4..^2] // [|2; 3|]

run() // Prints the same thing twice
```

Esse recurso implementa o [F # RFC FS-1076](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1076-from-the-end-slicing.md).

## <a name="preview-overloads-of-custom-keywords-in-computation-expressions"></a>Visualização: sobrecargas de palavras-chave personalizadas em expressões de computação

As expressões de computação são um recurso poderoso para autores de biblioteca e estrutura. Eles permitem que você aprimore significativamente a expressividade dos componentes, permitindo que você defina membros conhecidos e formate uma DSL para o domínio no qual você está trabalhando.

O F # 5 adiciona suporte à visualização para sobrecarregar operações personalizadas em expressões de computação. Ele permite que o seguinte código seja escrito e consumido:

```fsharp
open System

type InputKind =
    | Text of placeholder:string option
    | Password of placeholder: string option

type InputOptions =
  { Label: string option
    Kind : InputKind
    Validators : (string -> bool) array }

type InputBuilder() =
    member t.Yield(_) =
      { Label = None
        Kind = Text None
        Validators = [||] }

    [<CustomOperation("text")>]
    member this.Text(io, ?placeholder) =
        { io with Kind = Text placeholder }

    [<CustomOperation("password")>]
    member this.Password(io, ?placeholder) =
        { io with Kind = Password placeholder }

    [<CustomOperation("label")>]
    member this.Label(io, label) =
        { io with Label = Some label }

    [<CustomOperation("with_validators")>]
    member this.Validators(io, [<ParamArray>] validators) =
        { io with Validators = validators }

let input = InputBuilder()

let name =
    input {
    label "Name"
    text
    with_validators
        (String.IsNullOrWhiteSpace >> not)
    }

let email =
    input {
    label "Email"
    text "Your email"
    with_validators
        (String.IsNullOrWhiteSpace >> not)
        (fun s -> s.Contains "@")
    }

let password =
    input {
    label "Password"
    password "Must contains at least 6 characters, one number and one uppercase"
    with_validators
        (String.exists Char.IsUpper)
        (String.exists Char.IsDigit)
        (fun s -> s.Length >= 6)
    }
```

Antes dessa alteração, você poderia escrever o `InputBuilder` tipo como ele está, mas não poderia usá-lo da maneira como ele é usado no exemplo. Como as sobrecargas, os parâmetros opcionais e os `System.ParamArray` tipos Now são permitidos, tudo funciona exatamente como você esperaria.

Esse recurso implementa o [F # RFC FS-1056](https://github.com/fsharp/fslang-design/blob/master/preview/FS-1056-allow-custom-operation-overloads.md).
