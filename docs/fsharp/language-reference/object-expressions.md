---
title: Expressões de objeto
description: 'Saiba como usar expressões de objeto F # quando quiser evitar o código extra e a sobrecarga necessárias para criar um novo tipo nomeado.'
ms.date: 02/08/2019
ms.openlocfilehash: 8a3e40b7833b551eefb95ec62b935acd1ba7b1f9
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740296"
---
# <a name="object-expressions"></a>Expressões de objeto

Uma *expressão de objeto* é uma expressão que cria uma nova instância de um tipo de objeto anônimo criado dinamicamente com base em um tipo base, interface ou conjunto de interfaces existente.

## <a name="syntax"></a>Sintaxe

```fsharp
// When typename is a class:
{ new typename [type-params]arguments with
    member-definitions
    [ additional-interface-definitions ]
}
// When typename is not a class:
{ new typename [generic-type-args] with
    member-definitions
    [ additional-interface-definitions ]
}
```

## <a name="remarks"></a>Comentários

Na sintaxe anterior, o *TypeName* representa um tipo de classe ou de interface existente. o *tipo-params* descreve os parâmetros de tipo genérico opcionais. Os *argumentos* são usados somente para tipos de classe, que exigem parâmetros de construtor. As *definições de membro* são substituições de métodos de classe base ou implementações de métodos abstratos de uma classe base ou de uma interface.

O exemplo a seguir ilustra vários tipos diferentes de expressões de objeto.

```fsharp
// This object expression specifies a System.Object but overrides the
// ToString method.
let obj1 = { new System.Object() with member x.ToString() = "F#" }
printfn $"{obj1}"

// This object expression implements the IFormattable interface.
let delimiter(delim1: string, delim2: string, value: string) =
    { new System.IFormattable with
        member x.ToString(format: string, provider: System.IFormatProvider) =
            if format = "D" then
                delim1 + value + delim2
            else
                value }

let obj2 = delimiter("{","}", "Bananas!");

printfn "%A" (System.String.Format("{0:D}", obj2))

// Define two interfaces
type IFirst =
  abstract F : unit -> unit
  abstract G : unit -> unit

type ISecond =
  inherit IFirst
  abstract H : unit -> unit
  abstract J : unit -> unit

// This object expression implements both interfaces.
let implementer() =
    { new ISecond with
        member this.H() = ()
        member this.J() = ()
      interface IFirst with
        member this.F() = ()
        member this.G() = () }
```

## <a name="using-object-expressions"></a>Usando expressões de objeto

Você usa expressões de objeto quando deseja evitar o código extra e a sobrecarga necessária para criar um novo tipo nomeado. Se você usar expressões de objeto para minimizar o número de tipos criados em um programa, poderá reduzir o número de linhas de código e evitar a proliferação desnecessária de tipos. Em vez de criar vários tipos apenas para lidar com situações específicas, você pode usar uma expressão de objeto que personaliza um tipo existente ou fornece uma implementação apropriada de uma interface para o caso específico em questão.

## <a name="see-also"></a>Confira também

- [Referência de linguagem F #](index.md)
