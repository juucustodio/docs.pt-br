---
title: Tipos de valor anuláveis
description: 'Saiba como usar tipos de valor anulável, uma maneira de representar tipos de valor que também podem ser nulos, em F #.'
ms.date: 11/19/2020
ms.openlocfilehash: e28cbfc57c5631573f46ac36462517cf011e96d2
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009632"
---
# <a name="nullable-value-types"></a>Tipos de valor anuláveis

Um _tipo de valor anulável_ `Nullable<'T>` representa qualquer tipo de [struct](structures.md) que também pode ser `null` . Isso é útil ao interagir com bibliotecas e componentes que podem escolher representar esses tipos de tipos, como inteiros, com um `null` valor por motivos de eficiência. O tipo subjacente que faz backup desse constructo é <xref:System.Nullable%601?displayProperty=nameWithType> .

## <a name="syntax"></a>Syntax

```fsharp
Nullable<'T>
Nullable value
```

## <a name="declare-and-assign-with-values"></a>Declarar e atribuir com valores

Declarar um tipo de valor anulável é exatamente como declarar qualquer tipo de wrapper em F #:

```fsharp
open System

let x = 12
let nullableX = Nullable<int> x
```

Você também pode Elide o parâmetro de tipo genérico e permitir que a inferência de tipos o resolva:

```fsharp
open System

let x = 12
let nullableX = Nullable x
```

Para atribuir a um tipo de valor anulável, você também precisará ser explícito. Não há conversão implícita para tipos de valores anuláveis definidos em F #:

```fsharp
open System

let mutable x = Nullable 12
x <- Nullable 13
```

## <a name="assign-null"></a>Atribuir nulo

Não é possível atribuir diretamente `null` a um tipo de valor anulável. Use `Nullable()` em vez disso:

```fsharp
let mutable a = Nullable 42
a <- Nullable()
```

Isso ocorre porque `Nullable<'T>` o não tem `null` um valor adequado.

## <a name="pass-and-assign-to-members"></a>Passar e atribuir a membros

Uma diferença importante entre trabalhar com membros e valores F # é que os tipos de valores anuláveis podem ser inferidos implicitamente quando você estiver trabalhando com membros. Considere o seguinte método que usa um tipo de valor anulável como entrada:

```fsharp
type C() =
    member _.M(x: Nullable<int>) = x.HasValue
    member val NVT = Nullable 12 with get, set

let c = C()
c.M(12)
c.NVT <- 12
```

No exemplo anterior, você pode passar `12` para o método `M` . Você também pode atribuir `12` à propriedade auto `NVT` . Se a entrada puder ser construída como um tipo de valor anulável e corresponder ao tipo de destino, o compilador de F # converterá implicitamente tais chamadas ou atribuições.

## <a name="examine-a-nullable-value-type-instance"></a>Examinar uma instância de tipo de valor anulável

Ao contrário das [Opções](options.md), que são uma construção generalizada para representar um valor possível, os tipos de valores anuláveis não são usados com correspondência de padrões. Em vez disso, você precisa usar uma [`if`](conditional-expressions-if-then-else.md) expressão e verificar a `HasValue` propriedade.

Para obter o valor subjacente, use a `Value` propriedade após uma `HasValue` verificação, desta forma:

```fsharp
open System

let a = Nullable 42

if a.HasValue then
    printfn $"{a} is {a.Value}"
else
    printfn $"{a} has no value."
```

## <a name="nullable-operators"></a>Operadores anuláveis

As operações em tipos de valores anuláveis, como aritmética ou comparação, podem exigir o uso de [operadores anuláveis](symbol-and-operator-reference/nullable-operators.md).

Você pode converter de um tipo de valor anulável para outro usando operadores de conversão do `FSharp.Linq` namespace:

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt
```

Você também pode usar um operador não anulável apropriado para converter em um tipo primitivo, arriscando uma exceção se não tiver valor:

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt

printfn $"value is %f{float nullableFloat}"
```

Você também pode usar operadores anuláveis como um pequeno para verificar `HasValue` e `Value` :

```fsharp
open System
open FSharp.Linq

let nullableInt = Nullable 10
let nullableFloat = Nullable.float nullableInt

let isBigger = nullableFloat ?> 1.0
let isBiggerLongForm = nullableFloat.HasValue && nullableFloat.Value > 1.0
```

A `?>` comparação verifica se o lado esquerdo é anulável e só tem sucesso se tiver um valor. É equivalente à linha que a segue.

## <a name="see-also"></a>Confira também

- [Estruturas](structures.md)
- [Opções de F #](options.md)
