---
title: O que é F#
description: 'Saiba mais sobre o que é a linguagem de programação F # e qual é a programação em F #. Saiba mais sobre tipos de dados avançados, funções e como eles se encaixam juntos.'
ms.date: 08/03/2018
ms.openlocfilehash: a6bad3e1db63c3fe948b5916925d5eb24a18a41c
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739471"
---
# <a name="what-is-f"></a>O que é F\#

O F # é uma linguagem de programação funcional que torna mais fácil escrever código correto e passível de manutenção.

A programação F # envolve principalmente a definição de tipos e funções que são de tipo inferido e generalizados automaticamente. Isso permite que seu foco permaneça no domínio problemático e manipule seus dados, em vez dos detalhes da programação.

```fsharp
open System // Gets access to functionality in System namespace.

// Defines a function that takes a name and produces a greeting.
let getGreeting name = $"Hello, {name}! Isn't F# great?"

[<EntryPoint>]
let main args =
    // Defines a list of names
    let names = [ "Don"; "Julia"; "Xi" ]

    // Prints a greeting for each name!
    names
    |> List.map getGreeting
    |> List.iter (fun greeting -> printfn $"{greeting}")

    0
```

O F # tem vários recursos, incluindo:

* Sintaxe leve
* Imutável por padrão
* Inferência de tipos e generalização automática
* Funções de primeira classe
* Tipos de dados avançados
* Correspondência de padrões
* Programação assíncrona

Um conjunto completo de recursos está documentado na [referência de linguagem F #](./language-reference/index.md).

## <a name="rich-data-types"></a>Tipos de dados avançados

Tipos de dados como [registros](./language-reference/records.md) e [uniões discriminadas](./language-reference/discriminated-unions.md) permitem que você represente domínios e dados complexos.

```fsharp
// Group data with Records
type SuccessfulWithdrawal =
    { Amount: decimal
      Balance: decimal }

type FailedWithdrawal =
    { Amount: decimal
      Balance: decimal
      IsOverdraft: bool }

// Use discriminated unions to represent data of 1 or more forms
type WithdrawalResult =
    | Success of SuccessfulWithdrawal
    | InsufficientFunds of FailedWithdrawal
    | CardExpired of System.DateTime
    | UndisclosedFailure
```

Os registros F # e as uniões discriminadas são não nulos, imutáveis e comparáveis por padrão, tornando-os muito fáceis de usar.

## <a name="enforced-correctness-with-functions-and-pattern-matching"></a>Correção imposta com funções e correspondência de padrões

As funções de F # são fáceis de declarar e poderosas na prática. Quando combinado com [correspondência de padrões](./language-reference/pattern-matching.md), eles permitem que você defina o comportamento cuja exatidão é imposta pelo compilador.

```fsharp
// Returns a WithdrawalResult
let withdrawMoney amount = // Implementation elided

let handleWithdrawal amount =
    let w = withdrawMoney amount

    // The F# compiler enforces accounting for each case!
    match w with
    | Success s -> printfn "Successfully withdrew %f{s.Amount}"
    | InsufficientFunds f -> printfn "Failed: balance is %f{f.Balance}"
    | CardExpired d -> printfn "Failed: card expired on {d}"
    | UndisclosedFailure -> printfn "Failed: unknown :("
```

As funções F # também são de primeira classe, o que significa que elas podem ser passadas como parâmetros e retornadas de outras funções.

## <a name="functions-to-define-operations-on-objects"></a>Funções para definir operações em objetos

O F # tem suporte total para objetos, que são tipos de dados úteis quando você precisa misturar dados e funcionalidades. As funções F # são usadas para manipular objetos.

```fsharp
type Set<'T when 'T: comparison>(elements: seq<'T>) =
    member s.IsEmpty = // Implementation elided
    member s.Contains (value) =// Implementation elided
    member s.Add (value) = // Implementation elided
    // ...
    // Further Implementation elided
    // ...
    interface IEnumerable<‘T>
    interface IReadOnlyCollection<‘T>

module Set =
    let isEmpty (set: Set<'T>) = set.IsEmpty

    let contains element (set: Set<'T>) = set.Contains(element)

    let add value (set: Set<'T>) = set.Add(value)
```

Em vez de escrever código orientado a objeto, em F #, você geralmente escreverá um código que trata os objetos como outro tipo de dados para funções a serem manipuladas. Recursos como [interfaces genéricas](./language-reference/interfaces.md), [expressões de objeto](./language-reference/object-expressions.md)e uso criterioso de [Membros](./language-reference/members/index.md) são comuns em programas em F # maiores.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre um conjunto maior de recursos do F #, confira o [Tour em f #](tour.md).
