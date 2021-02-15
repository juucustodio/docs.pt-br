---
title: Resultados
description: "Saiba como usar o tipo ' Result ' de F # para ajudá-lo a escrever código tolerante a erros."
ms.date: 08/13/2020
ms.openlocfilehash: 53b1db0c9224ae032d58c06cd3c58e3dbed03f7b
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740218"
---
# <a name="results"></a>Resultados

O `Result<'T,'TFailure>` tipo permite que você grave código tolerante a erros que pode ser composto.

## <a name="syntax"></a>Sintaxe

```fsharp
// The definition of Result in FSharp.Core
[<StructuralEquality; StructuralComparison>]
[<CompiledName("FSharpResult`2")>]
[<Struct>]
type Result<'T,'TError> =
    | Ok of ResultValue:'T
    | Error of ErrorValue:'TError
```

## <a name="remarks"></a>Comentários

Consulte o [`Result`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-resultmodule.html) módulo para os combinadores internos para o `Result` . Escreva.

Observe que o tipo de resultado é uma [união discriminada de struct](discriminated-unions.md#struct-discriminated-unions). A semântica de igualdade estrutural se aplica aqui.

O `Result` tipo é normalmente usado no tratamento de erros do monadic, que geralmente é conhecido como [programação orientada por ferrovia](https://swlaschin.gitbooks.io/fsharpforfunandprofit/content/posts/recipe-part2.html) na Comunidade do F #.  O exemplo trivial a seguir demonstra essa abordagem.

```fsharp
// Define a simple type which has fields that can be validated
type Request =
    { Name: string
      Email: string }

// Define some logic for what defines a valid name.
//
// Generates a Result which is an Ok if the name validates;
// otherwise, it generates a Result which is an Error.
let validateName req =
    match req.Name with
    | null -> Error "No name found."
    | "" -> Error "Name is empty."
    | "bananas" -> Error "Bananas is not a name."
    | _ -> Ok req

// Similarly, define some email validation logic.
let validateEmail req =
    match req.Email with
    | null -> Error "No email found."
    | "" -> Error "Email is empty."
    | s when s.EndsWith("bananas.com") -> Error "No email from bananas.com is allowed."
    | _ -> Ok req

let validateRequest reqResult =
    reqResult
    |> Result.bind validateName
    |> Result.bind validateEmail

let test() =
    // Now, create a Request and pattern match on the result.
    let req1 = { Name = "Phillip"; Email = "phillip@contoso.biz" }
    let res1 = validateRequest (Ok req1)
    match res1 with
    | Ok req -> printfn $"My request was valid! Name: {req.Name} Email {req.Email}"  
    | Error e -> printfn $"Error: {e}"
    // Prints: "My request was valid!  Name: Phillip Email: phillip@consoto.biz"

    let req2 = { Name = "Phillip"; Email = "phillip@bananas.com" }
    let res2 = validateRequest (Ok req2)
    match res2 with
    | Ok req -> printfn $"My request was valid! Name: {req.Name} Email {req.Email}"  
    | Error e -> printfn $"Error: {e}"
    // Prints: "Error: No email from bananas.com is allowed."

test()
```

Como você pode ver, é muito fácil encadear várias funções de validação se você forçá-las a retornar um `Result` .  Isso permite que você divida a funcionalidade como esta em pequenas partes, que são tão combináveis quanto você precisa delas.  Isso também tem o valor agregado de *impor* o uso da [correspondência de padrões](pattern-matching.md) no final de uma rodada de validação, o que, por sua vez, impõe um grau mais alto de exatidão do programa.

## <a name="see-also"></a>Confira também

- [Uniões discriminadas](discriminated-unions.md)
- [Correspondência padrão](pattern-matching.md)
