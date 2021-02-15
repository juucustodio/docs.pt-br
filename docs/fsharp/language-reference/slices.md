---
title: Fatias
description: 'Saiba como usar fatias para tipos de dados F # existentes e como definir suas próprias fatias para outros tipos de dados.'
ms.date: 11/20/2020
ms.openlocfilehash: b776058df5a174dfe48dbf513bf17281036dd83e
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740374"
---
# <a name="slices"></a>Fatias

Este artigo explica como tirar fatias de tipos existentes de F # e como definir suas próprias fatias.

Em F #, uma fatia é um subconjunto de qualquer tipo de dados.  As fatias são semelhantes aos [indexadores](./members/indexed-properties.md), mas em vez de produzir um único valor da estrutura de dados subjacente, elas produzem várias delas. As fatias usam a `..` sintaxe do operador para selecionar o intervalo de índices especificados em um tipo de dados. Para obter mais informações, consulte o [artigo referência de expressões de looping](./loops-for-in-expression.md).

O F # atualmente tem suporte intrínseco para cadeias de caracteres de divisão, listas, matrizes e matrizes multidimensionais (2D, 3D, 4D). A divisão é mais comumente usada com matrizes e listas de F #. Você pode adicionar fatias a seus tipos de dados personalizados usando o `GetSlice` método em sua definição de tipo ou em uma extensão de [tipo](type-extensions.md)no escopo.

## <a name="slicing-f-lists-and-arrays"></a>Divisão de listas e matrizes de F #

Os tipos de dados mais comuns que são segmentados são listas e matrizes de F #.  O exemplo a seguir demonstra como segmentar listas:

```fsharp
// Generate a list of 100 integers
let fullList = [ 1 .. 100 ]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullList.[1..5]
printfn $"Small slice: {smallSlice}"

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullList.[..5]
printfn $"Unbounded beginning slice: {unboundedBeginning}"

// Create a slice from an index to the end of the list
let unboundedEnd = fullList.[94..]
printfn $"Unbounded end slice: {unboundedEnd}"
```

As matrizes de divisão são apenas como listas de fatias:

```fsharp
// Generate an array of 100 integers
let fullArray = [| 1 .. 100 |]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullArray.[1..5]
printfn $"Small slice: {smallSlice}"

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullArray.[..5]
printfn $"Unbounded beginning slice: {unboundedBeginning}"

// Create a slice from an index to the end of the list
let unboundedEnd = fullArray.[94..]
printfn $"Unbounded end slice: {unboundedEnd}"
```

## <a name="slicing-multidimensional-arrays"></a>Fatiando matrizes multidimensionais

O f # dá suporte a matrizes multidimensionais na biblioteca principal do F #. Assim como acontece com matrizes unidimensionais, as fatias de matrizes multidimensionais também podem ser úteis. No entanto, a introdução de dimensões adicionais exige uma sintaxe ligeiramente diferente para que você possa colocar fatias de linhas e colunas específicas.

Os exemplos a seguir demonstram como dividir uma matriz 2D:

```fsharp
// Generate a 3x3 2D matrix
let A = array2D [[1;2;3];[4;5;6];[7;8;9]]
printfn $"Full matrix:\n {A}"

// Take the first row
let row0 = A.[0,*]
printfn $"{row0}"

// Take the first column
let col0 = A.[*,0]
printfn $"{col0}"

// Take all rows but only two columns
let subA = A.[*,0..1]
printfn $"{subA}"

// Take two rows and all columns
let subA' = A.[0..1,*]
printfn $"{subA}"

// Slice a 2x2 matrix out of the full 3x3 matrix
let twoByTwo = A.[0..1,0..1]
printfn $"{twoByTwo}"
```

## <a name="defining-slices-for-other-data-structures"></a>Definindo fatias para outras estruturas de dados

A biblioteca de núcleos F # define fatias para um conjunto limitado de tipos. Se você quiser definir fatias para mais tipos de dados, poderá fazer isso na própria definição de tipo ou em uma extensão de tipo.

Por exemplo, veja como você pode definir fatias para a <xref:System.ArraySegment%601> classe para permitir uma manipulação de dados conveniente:

```fsharp
open System

type ArraySegment<'TItem> with
    member segment.GetSlice(start, finish) =
        let start = defaultArg start 0
        let finish = defaultArg finish segment.Count
        ArraySegment(segment.Array, segment.Offset + start, finish - start)

let arr = ArraySegment [| 1 .. 10 |]
let slice = arr.[2..5] //[ 3; 4; 5]
```

Outro exemplo que usa <xref:System.Span%601> os <xref:System.ReadOnlySpan%601> tipos e:

```fsharp
open System

type ReadOnlySpan<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

type Span<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn $"{arr}"

let sp = [| 1; 2; 3; 4; 5 |].AsSpan()
printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
printSpan sp.[..5] // [|1; 2; 3; 4; 5|]
printSpan sp.[0..3] // [|1; 2; 3|]
printSpan sp.[1..3] // |2; 3|]
```

## <a name="built-in-f-slices-are-end-inclusive"></a>As fatias F # internas são inclusivas

Todas as fatias intrínsecas em F # são inclusivas; ou seja, o limite superior é incluído na fatia. Para uma determinada fatia com índice inicial `x` e índice final `y` , a fatia resultante incluirá o valor *YTH* .

```fsharp
// Define a new list
let xs = [1 .. 10]

printfn $"{xs.[2..5]}" // Includes the 5th index
```

## <a name="built-in-f-empty-slices"></a>Fatias internas F # vazias

As listas de F #, matrizes, sequências, cadeias de caracteres, matrizes multidimensionais (2D, 3D, 4D) produzirão uma fatia vazia se a sintaxe puder produzir uma fatia que não existe.

Considere o seguinte exemplo:

```fsharp
let l = [ 1..10 ]
let a = [| 1..10 |]
let s = "hello!"

let emptyList = l.[-2..(-1)]
let emptyArray = a.[-2..(-1)]
let emptyString = s.[-2..(-1)]
```

> [!IMPORTANT]
> Os desenvolvedores de C# podem esperar que eles lancem uma exceção em vez de produzir uma fatia vazia. Essa é uma decisão de design enraizada no fato de que coleções vazias compõem em F #. Uma lista de F # vazia pode ser composta com outra lista de F #, uma cadeia de caracteres vazia pode ser adicionada a uma cadeia de caracteres existente e assim por diante. Pode ser comum pegar fatias com base em valores passados como parâmetros, e ser tolerante a fora dos limites > por meio da produção de uma coleção vazia cabe à natureza composicional do código F #.

## <a name="fixed-index-slices-for-3d-and-4d-arrays"></a>Fatias de índice fixo para matrizes 3D e 4D

Para matrizes F # 3D e 4D, você pode "corrigir" um índice específico e fatiar outras dimensões com esse índice fixo.

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

Se você quiser extrair a fatia `[| 4; 5 |]` da matriz, use uma fatia de índice fixo.

```fsharp
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

A última linha corrige os `y` `z` índices e da matriz 3D e leva o restante dos `x` valores que correspondem à matriz.

## <a name="see-also"></a>Confira também

- [Propriedades indexadas](./members/indexed-properties.md)
