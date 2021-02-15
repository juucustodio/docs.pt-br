---
title: Nameof
description: Saiba mais sobre o operador nameof, um recurso de metaprogramação que permite que você produza o nome de qualquer símbolo em seu código-fonte.
ms.date: 11/12/2020
ms.openlocfilehash: 9947d7172d1b73db5c181297ec8b1131382e1f5e
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94688598"
---
# <a name="nameof"></a>Nameof

A `nameof` expressão produz uma constante de cadeia de caracteres que corresponde ao nome na origem de quase qualquer construção F # na origem.

## <a name="syntax"></a>Sintaxe

```fsharp
nameof symbol
nameof<'TGeneric>
```

## <a name="remarks"></a>Comentários

`nameof` funciona resolvendo o símbolo passado para ele e produz o nome desse símbolo como ele é declarado em seu código-fonte. Isso é útil em vários cenários, como registro em log e protege o registro em log contra alterações no código-fonte.

```fsharp
let months =
    [
        "January"; "February"; "March"; "April";
        "May"; "June"; "July"; "August"; "September";
        "October"; "November"; "December"
    ]

let lookupMonth month =
    if (month > 12 || month < 1) then
        invalidArg (nameof month) ($"Value passed in was %d{month}.")

    months.[month-1]

printfn "%s" (lookupMonth 12)
printfn "%s" (lookupMonth 1)
printfn "%s" (lookupMonth 13)
```

A última linha gerará uma exceção e `"month"` será mostrada na mensagem de erro.

Você pode usar um nome de quase todas as construções em F #:

```fsharp
module M =
    let f x = nameof x

printfn $"{(M.f 12)]}"
printfn $"{(nameof M)}"
printfn $"{(nameof M.f)}"
```

`nameof` Não é uma função de primeira classe e não pode ser usada como tal. Isso significa que ele não pode ser parcialmente aplicado e os valores não podem ser redirecionados para ele por meio de operadores de pipeline de F #.

## <a name="nameof-on-operators"></a>Nameof em operadores

Os operadores em F # podem ser usados de duas maneiras, como um texto de operador ou um símbolo que representa o formulário compilado. `nameof` em um operador produzirá o nome do operador como ele é declarado na origem. Para obter o nome compilado, use o nome compilado em Source:

```fsharp
nameof(+) // "+"
nameof op_Addition // "op_Addition"
```

## <a name="nameof-on-generics"></a>Nameof em genéricos

Você também pode usar um nome de parâmetro de tipo genérico, mas a sintaxe é diferente:

```fsharp
let f<'a> () = nameof<'a>
f() // "a"
```

`nameof<'TGeneric>` obterá o nome do símbolo conforme definido em Source, não o nome do tipo substituído em um site de chamada.

O motivo pelo qual a sintaxe é diferente é alinhar com outros operadores intrínsecos em F # como `typeof<>` e `typedefof<>` . Isso torna o F # consistente com relação aos operadores que atuam em tipos genéricos e qualquer outra coisa na origem.

## <a name="nameof-in-pattern-matching"></a>Nameof na correspondência de padrões

O [ `nameof` padrão](pattern-matching.md#nameof-pattern) permite que você use `nameof` em uma expressão de correspondência de padrões como esta:

```fsharp
let f (str: string) =
    match str with
    | nameof str -> "It's 'str'!"
    | _ -> "It is not 'str'!"

f "str" // matches
f "asdf" // does not match
```
