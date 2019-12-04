---
title: O que há de F# novo no F# guia de 4,6
description: Obtenha uma visão geral dos novos recursos disponíveis em F# 4,6.
ms.date: 11/27/2019
ms.openlocfilehash: 81d3e988d044cb16f8ec079118fd0ede2dabc587
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74644078"
---
# <a name="whats-new-in-f-46"></a><span data-ttu-id="582b8-103">O que há de F# novo no 4,6</span><span class="sxs-lookup"><span data-stu-id="582b8-103">What's new in F# 4.6</span></span>

<span data-ttu-id="582b8-104">F#4,6 adiciona várias melhorias ao F# idioma.</span><span class="sxs-lookup"><span data-stu-id="582b8-104">F# 4.6 adds multiple improvements to the F# language.</span></span>

## <a name="get-started"></a><span data-ttu-id="582b8-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="582b8-105">Get started</span></span>

<span data-ttu-id="582b8-106">F#o 4,6 está disponível em todas as distribuições do .NET Core e ferramentas do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="582b8-106">F# 4.6 is available in all .NET Core distributions and Visual Studio tooling.</span></span> <span data-ttu-id="582b8-107">[Introdução F# ](../get-started/index.md) ao para saber mais.</span><span class="sxs-lookup"><span data-stu-id="582b8-107">[Get started with F#](../get-started/index.md) to learn more.</span></span>

## <a name="anonymous-records"></a><span data-ttu-id="582b8-108">Registros anônimos</span><span class="sxs-lookup"><span data-stu-id="582b8-108">Anonymous records</span></span>

<span data-ttu-id="582b8-109">Os [registros anônimos](../language-reference/anonymous-records.md) são um novo F# tipo apresentado em F# 4,6.</span><span class="sxs-lookup"><span data-stu-id="582b8-109">[Anonymous records](../language-reference/anonymous-records.md) are a new kind of F# type introduced in F# 4.6.</span></span> <span data-ttu-id="582b8-110">Eles são agregações simples de valores nomeados que não precisam ser declarados antes do uso.</span><span class="sxs-lookup"><span data-stu-id="582b8-110">They are simple aggregates of named values that don't need to be declared before use.</span></span> <span data-ttu-id="582b8-111">Você pode declará-los como structs ou tipos de referência.</span><span class="sxs-lookup"><span data-stu-id="582b8-111">You can declare them as either structs or reference types.</span></span> <span data-ttu-id="582b8-112">Eles são tipos de referência por padrão.</span><span class="sxs-lookup"><span data-stu-id="582b8-112">They're reference types by default.</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

<span data-ttu-id="582b8-113">Eles também podem ser declarados como structs para quando você deseja agrupar tipos de valor e estão operando em cenários sensíveis ao desempenho:</span><span class="sxs-lookup"><span data-stu-id="582b8-113">They can also be declared as structs for when you want to group value types and are operating in performance-sensitive scenarios:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    struct {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

<span data-ttu-id="582b8-114">Elas são muito poderosas e podem ser usadas em vários cenários.</span><span class="sxs-lookup"><span data-stu-id="582b8-114">They're quite powerful and can be used in numerous scenarios.</span></span> <span data-ttu-id="582b8-115">Saiba mais em [registros anônimos](../language-reference/anonymous-records.md).</span><span class="sxs-lookup"><span data-stu-id="582b8-115">Learn more at [Anonymous records](../language-reference/anonymous-records.md).</span></span>

## <a name="valueoption-functions"></a><span data-ttu-id="582b8-116">Funções ValueOption</span><span class="sxs-lookup"><span data-stu-id="582b8-116">ValueOption functions</span></span>

<span data-ttu-id="582b8-117">O tipo ValueOption adicionado em F# 4,5 agora tem "paridade de função associada a módulo" com o tipo de opção.</span><span class="sxs-lookup"><span data-stu-id="582b8-117">The ValueOption type added in F# 4.5 now has "module-bound function parity" with the Option type.</span></span> <span data-ttu-id="582b8-118">Alguns dos exemplos mais comumente usados são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="582b8-118">Some of the more commonly-used examples are as follows:</span></span>

```fsharp
// Multiply a value option by 2 if it has  value
let xOpt = ValueSome 99
let result = xOpt |> ValueOption.map (fun v -> v * 2)

// Reverse a string if it exists
let strOpt = ValueSome "Mirror image"
let reverse (str: string) =
    match str with
    | null
    | "" -> None
    | s ->
        str.ToCharArray()
        |> Array.rev
        |> string
        |> Some

let reversedString = strOpt |> Option.bind reverse
```

<span data-ttu-id="582b8-119">Isso permite que o ValueOption seja usado exatamente como a opção em cenários em que um tipo de valor melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="582b8-119">This allows for ValueOption to be used just like Option in scenarios where having a value type improves performance.</span></span>