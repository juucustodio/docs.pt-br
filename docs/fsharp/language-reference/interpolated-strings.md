---
title: Cadeias de caracteres interpoladas
description: 'Saiba mais sobre cadeias interpoladas, uma forma especial de cadeia de caracteres que permite inserir expressões F # diretamente dentro delas.'
ms.date: 11/12/2020
ms.openlocfilehash: 8c552b44cea7d6c51ec333b6bdd4d407c6f10da7
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829681"
---
# <a name="interpolated-strings"></a>Cadeias de caracteres interpoladas

Cadeias de caracteres interpoladas são [cadeias de caracteres](strings.md) que permitem inserir expressões F # nelas. Eles são úteis em uma ampla gama de cenários em que o valor de uma cadeia de caracteres pode ser alterado com base no resultado de um valor ou expressão.

## <a name="syntax"></a>Sintaxe

```fsharp
$"string-text {expr}"
$"string-text %format-specifier{expr}"
$"""string-text {"embedded string literal"}"""
```

## <a name="remarks"></a>Comentários

As cadeias de caracteres interpoladas permitem escrever código em "buracos" dentro de um literal de cadeia de caracteres. Este é um exemplo básico:

```fsharp
let name = "Phillip"
let age = 30
printfn $"Name: {name}, Age: {age}"

printfn $"I think {3.0 + 0.14} is close to {System.Math.PI}!"
```

O conteúdo entre cada `{}` par de chaves pode ser qualquer expressão F #.

Para escapar de um `{}` par de chaves, escreva dois deles da seguinte forma:

```fsharp
let str = $"A pair of braces: {{}}"
// "A pair of braces: {}"
```

## <a name="typed-interpolated-strings"></a>Cadeias de caracteres interpoladas com tipo

As cadeias de caracteres interpoladas também podem ter especificadores de formato F # para impor a segurança de tipo.

```fsharp
let name = "Phillip"
let age = 30

printfn $"Name: %s{name}, Age: %d{age}"

// Error: type mismatch
printfn $"Name: %s{age}, Age: %d{name}"
```

No exemplo anterior, o código transmite erroneamente o `age` valor onde `name` deveria ser, e vice-versa. Como as cadeias de caracteres interpoladas usam especificadores de formato, esse é um erro de compilação em vez de um bug de tempo de execução sutil.

Todos os especificadores de formato abordados na [formatação de texto sem formatação](plaintext-formatting.md) são válidos dentro de uma cadeia de caracteres interpolada.

## <a name="verbatim-interpolated-strings"></a>Cadeias de caracteres interpoladas literalmente

O F # dá suporte a cadeias de caracteres interpoladas literalmente com aspas triplas para que você possa inserir literais de cadeia.

```fsharp
let age = 30

printfn $"""Name: {"Phillip"}, Age: %d{age}"""
```

## <a name="aligning-expressions-in-interpolated-strings"></a>Alinhando expressões em cadeias de caracteres interpoladas

Você pode alinhar as expressões à esquerda ou alinhadas à direita dentro de cadeias interpoladas com `|` e uma especificação de quantos espaços. A cadeia de caracteres interpolada a seguir alinha as expressões esquerda e direita à esquerda e à direita, respectivamente, por sete espaços.

```fsharp
printfn $"""|{"Left",-7}|{"Right",7}|"""
// |Left   |  Right|
```

## <a name="interpolated-strings-and-formattablestring-formatting"></a>Cadeias de caracteres interpoladas e `FormattableString` formatação

Você também pode aplicar a formatação que segue as regras para <xref:System.FormattableString> :

```fsharp
let speedOfLight = 299792.458
printfn $"The speed of light is {speedOfLight:N3} km/s."
// "The speed of light is 299,792.458 km/s."
```

Além disso, uma cadeia de caracteres interpolada também pode ser o tipo marcado como um <xref:System.FormattableString> por meio de uma anotação de tipo:

```fsharp
let frmtStr = $"The speed of light is {speedOfLight:N3} km/s." : FormattableString
// Type: FormattableString
// The speed of light is 299,792.458 km/s.
```

Observe que a anotação de tipo deve estar na própria expressão de cadeia de caracteres interpolada. O F # não converte implicitamente uma cadeia de caracteres interpolada em um <xref:System.FormattableString> .

## <a name="see-also"></a>Confira também

* [Cadeias de caracteres](strings.md)
