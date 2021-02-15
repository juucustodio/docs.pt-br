---
title: Uniões discriminadas
description: 'Saiba como usar as uniões discriminadas em F #.'
ms.date: 08/15/2020
ms.openlocfilehash: f90ac2c2ea21182cf5fd3657d2ada00a763139fe
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740231"
---
# <a name="discriminated-unions"></a>Uniões discriminadas

Uniões discriminadas fornecem suporte para valores que podem ser um de vários casos nomeados, possivelmente cada um com valores e tipos diferentes. Uniões discriminadas são úteis para dados heterogêneos; dados que podem ter casos especiais, incluindo casos de erro e válidos; dados que variam em tipo de uma instância para outra; e como uma alternativa para hierarquias de objetos pequenos. Além disso, as uniões discriminadas recursivas são usadas para representar estruturas de dados de árvore.

## <a name="syntax"></a>Sintaxe

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    | case-identifier1 [of [ fieldname1 : ] type1 [ * [ fieldname2 : ] type2 ...]
    | case-identifier2 [of [fieldname3 : ]type3 [ * [ fieldname4 : ]type4 ...]

    [ member-list ]
```

## <a name="remarks"></a>Comentários

Uniões discriminadas são semelhantes aos tipos Union em outras linguagens, mas há diferenças. Como com um tipo de União em C++ ou um tipo de variante em Visual Basic, os dados armazenados no valor não são fixos; pode ser uma das várias opções distintas. No entanto, ao contrário das uniões nessas outras linguagens, cada uma das opções possíveis recebe um *identificador de caso*. Os identificadores de caso são nomes para os vários tipos possíveis de valores que os objetos desse tipo podem ser; os valores são opcionais. Se os valores não estiverem presentes, o caso será equivalente a um caso de enumeração. Se os valores estiverem presentes, cada valor poderá ser um único valor de um tipo especificado ou uma tupla que agrega vários campos dos mesmos ou de tipos diferentes. Você pode dar um nome a um campo individual, mas o nome é opcional, mesmo que outros campos no mesmo caso sejam nomeados.

A acessibilidade para uniões discriminadas usa como padrão `public` .

Por exemplo, considere a declaração a seguir de um tipo de forma.

```fsharp
type Shape =
    | Rectangle of width : float * length : float
    | Circle of radius : float
    | Prism of width : float * float * height : float
```

O código anterior declara uma forma de união discriminada, que pode ter valores de qualquer um dos três casos: Rectangle, Circle e Prism. Cada caso tem um conjunto diferente de campos. O caso de retângulo tem dois campos nomeados, ambos os tipos `float` , que têm a largura e o comprimento dos nomes. O caso de círculo tem apenas um campo nomeado, raio. O caso do prisma tem três campos, dois dos quais (largura e altura) são campos nomeados. Os campos sem nome são referidos como campos anônimos.

Você constrói objetos fornecendo valores para os campos nomeados e anônimos de acordo com os exemplos a seguir.

```fsharp
let rect = Rectangle(length = 1.3, width = 10.0)
let circ = Circle (1.0)
let prism = Prism(5., 2.0, height = 3.0)
```

Esse código mostra que você pode usar os campos nomeados na inicialização ou pode contar com a ordenação dos campos na declaração e apenas fornecer os valores para cada campo por vez. A chamada de construtor para `rect` no código anterior usa os campos nomeados, mas a chamada de construtor para `circ` usa a ordenação. Você pode misturar os campos ordenados e os campos nomeados, como na construção de `prism` .

O `option` tipo é uma união discriminada simples na biblioteca principal do F #. O `option` tipo é declarado da seguinte maneira.

```fsharp
// The option type is a discriminated union.
type Option<'a> =
    | Some of 'a
    | None
```

O código anterior especifica que o tipo `Option` é uma união discriminada que tem dois casos `Some` e `None` . O `Some` caso tem um valor associado que consiste em um campo anônimo cujo tipo é representado pelo parâmetro de tipo `'a` . O `None` caso não tem nenhum valor associado. Portanto, o `option` tipo especifica um tipo genérico que tem um valor de algum tipo ou nenhum valor. O tipo `Option` também tem um alias de tipo minúsculo, `option` , que é mais comumente usado.

Os identificadores de caso podem ser usados como construtores para o tipo de união discriminada. Por exemplo, o código a seguir é usado para criar valores do `option` tipo.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2001.fs)]

Os identificadores de caso também são usados em expressões de correspondência de padrões. Em uma expressão de correspondência de padrões, os identificadores são fornecidos para os valores associados aos casos individuais. Por exemplo, no código a seguir, `x` é o identificador dado ao valor associado ao `Some` caso do `option` tipo.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2002.fs)]

Em expressões de correspondência de padrões, você pode usar campos nomeados para especificar correspondências de União discriminadas. Para o tipo de forma que foi declarado anteriormente, você pode usar os campos nomeados como mostra o código a seguir para extrair os valores dos campos.

```fsharp
let getShapeWidth shape =
    match shape with
    | Rectangle(width = w) -> w
    | Circle(radius = r) -> 2. * r
    | Prism(width = w) -> w
```

Normalmente, os identificadores de caso podem ser usados sem qualificá-los com o nome da União. Se desejar que o nome sempre seja qualificado com o nome da União, você poderá aplicar o atributo [RequireQualifiedAccess](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html) à definição do tipo Union.

### <a name="unwrapping-discriminated-unions"></a>Desencapsular uniões discriminadas

Nas uniões discriminadas em F # são geralmente usadas em modelagem de domínio para encapsular um único tipo. Também é fácil extrair o valor subjacente por meio de correspondência de padrões. Você não precisa usar uma expressão de correspondência para um único caso:

```fsharp
let ([UnionCaseIdentifier] [values]) = [UnionValue]
```

O exemplo a seguir demonstra este:

```fsharp
type ShaderProgram = | ShaderProgram of id:int

let someFunctionUsingShaderProgram shaderProgram =
    let (ShaderProgram id) = shaderProgram
    // Use the unwrapped value
    ...
```

A correspondência de padrões também é permitida diretamente em parâmetros de função, para que você possa desencapsular um único caso:

```fsharp
let someFunctionUsingShaderProgram (ShaderProgram id) =
    // Use the unwrapped value
    ...
```

## <a name="struct-discriminated-unions"></a>Uniões discriminadas de struct

Você também pode representar uniões discriminadas como estruturas.  Isso é feito com o `[<Struct>]` atributo.

```fsharp
[<Struct>]
type SingleCase = Case of string

[<Struct>]
type Multicase =
    | Case1 of Case1 : string
    | Case2 of Case2 : int
    | Case3 of Case3 : double
```

Como esses são tipos de valor e não tipos de referência, há considerações extras em comparação com as uniões discriminadas de referência:

1. Eles são copiados como tipos de valor e têm semântica de tipo de valor.
2. Você não pode usar uma definição de tipo recursiva com uma união discriminada de struct com multicaixa.
3. Você deve fornecer nomes de caso exclusivos para uma união discriminada de struct com multicaixa.

## <a name="using-discriminated-unions-instead-of-object-hierarchies"></a>Usando uniões discriminadas em vez de hierarquias de objeto

Geralmente, você pode usar uma união discriminada como uma alternativa mais simples a uma pequena hierarquia de objetos. Por exemplo, a seguinte união discriminada pode ser usada em vez de uma `Shape` classe base que tenha tipos derivados para Circle, Square e assim por diante.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2003.fs)]

Em vez de um método virtual para computar uma área ou um perímetro, como você usaria em uma implementação orientada a objeto, você pode usar a correspondência de padrões para ramificar para fórmulas apropriadas para computar essas quantidades. No exemplo a seguir, fórmulas diferentes são usadas para calcular a área, dependendo da forma.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2004.fs)]

A saída é da seguinte maneira:

```console
Area of circle that has radius 15.000000: 706.858347
Area of square that has side 10.000000: 100.000000
Area of rectangle that has height 5.000000 and width 10.000000 is 50.000000
```

## <a name="using-discriminated-unions-for-tree-data-structures"></a>Usando uniões discriminadas para estruturas de dados de árvore

Uniões discriminadas podem ser recursivas, o que significa que a União em si pode ser incluída no tipo de um ou mais casos. As uniões discriminadas recursivas podem ser usadas para criar estruturas de árvore, que são usadas para modelar expressões em linguagens de programação. No código a seguir, uma união discriminada recursiva é usada para criar uma estrutura de dados de árvore binária. A União consiste em dois casos, `Node` , que é um nó com um valor inteiro e subárvores esquerda e direita, e `Tip` que encerra a árvore.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2005.fs)]

No código anterior, `resultSumTree` tem o valor 10. A ilustração a seguir mostra a estrutura de árvore do `myTree` .

![Diagrama que mostra a estrutura de árvore para myTree.](../media/discriminated-unions/tree-structure-mytree.png)

Uniões discriminadas funcionam bem se os nós na árvore forem heterogêneos. No código a seguir, o tipo `Expression` representa a árvore de sintaxe abstrata de uma expressão em uma linguagem de programação simples que dá suporte à adição e à multiplicação de números e variáveis. Alguns dos casos de União não são recursivos e representam números ( `Number` ) ou variáveis ( `Variable` ). Outros casos são recursivos e representam operações ( `Add` e `Multiply` ), em que os operandos também são expressões. A `Evaluate` função usa uma expressão de correspondência para processar recursivamente a árvore de sintaxe.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2006.fs)]

Quando esse código é executado, o valor de `result` é 5.

## <a name="members"></a>Membros

É possível definir membros em uniões discriminadas. O exemplo a seguir mostra como definir uma propriedade e implementar uma interface:

```fsharp
open System

type IPrintable =
    abstract Print: unit -> unit

type Shape =
    | Circle of float
    | EquilateralTriangle of float
    | Square of float
    | Rectangle of float * float

    member this.Area =
        match this with
        | Circle r -> 2.0 * Math.PI * r
        | EquilateralTriangle s -> s * s * sqrt 3.0 / 4.0
        | Square s -> s * s
        | Rectangle(l, w) -> l * w

    interface IPrintable with
        member this.Print () =
            match this with
            | Circle r -> printfn $"Circle with radius %f{r}"
            | EquilateralTriangle s -> printfn $"Equilateral Triangle of side %f{s}"
            | Square s -> printfn $"Square with side %f{s}"
            | Rectangle(l, w) -> printfn $"Rectangle with length %f{l} and width %f{w}"
```

## <a name="common-attributes"></a>Atributos comuns

Os seguintes atributos são normalmente vistos em uniões discriminadas:

- `[<RequireQualifiedAccess>]`
- `[<NoEquality>]`
- `[<NoComparison>]`
- `[<Struct>]`

## <a name="see-also"></a>Confira também

- [Referência de linguagem F #](index.md)
