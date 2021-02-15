---
title: Tipos de enumeração-referência C#
description: Saiba mais sobre tipos de enumeração C# que representam uma opção ou uma combinação de opções
ms.date: 12/13/2019
f1_keywords:
- enum
- enum_CSharpKeyword
helpviewer_keywords:
- enum keyword [C#]
- enum type [C#]
- enumeration type [C#]
- bit flags [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
ms.openlocfilehash: a21bdf63247dc5fec95922de017e1d3502e08565
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599428"
---
# <a name="enumeration-types-c-reference"></a>Tipos de enumeração (referência C#)

Um *tipo de enumeração* (ou *tipo* de enumeração) é um [tipo de valor](value-types.md) definido por um conjunto de constantes nomeadas do tipo [numérico integral](integral-numeric-types.md) subjacente. Para definir um tipo de enumeração, use a `enum` palavra-chave e especifique os nomes dos *membros de enumeração*:

```csharp
enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter
}
```

Por padrão, os valores constantes associados de membros de enumeração são do tipo `int` ; eles começam com zero e aumentam em um seguindo a ordem de texto de definição. Você pode especificar explicitamente qualquer outro tipo [numérico integral](integral-numeric-types.md) como um tipo subjacente de um tipo de enumeração. Você também pode especificar explicitamente os valores constantes associados, como mostra o exemplo a seguir:

```csharp
enum ErrorCode : ushort
{
    None = 0,
    Unknown = 1,
    ConnectionLost = 100,
    OutlierReading = 200
}
```

Você não pode definir um método dentro da definição de um tipo de enumeração. Para adicionar funcionalidade a um tipo de enumeração, crie um [método de extensão](../../programming-guide/classes-and-structs/extension-methods.md).

O valor padrão de um tipo de enumeração `E` é o valor produzido por expressão `(E)0` , mesmo se zero não tiver o membro enum correspondente.

Você usa um tipo de enumeração para representar uma escolha de um conjunto de valores mutuamente exclusivos ou uma combinação de opções. Para representar uma combinação de opções, defina um tipo de enumeração como sinalizadores de bits.

## <a name="enumeration-types-as-bit-flags"></a>Tipos de Enumeração como Sinalizadores de Bit

Se você quiser que um tipo de enumeração represente uma combinação de opções, defina membros de enum para essas opções, de modo que uma opção individual seja um campo de bits. Ou seja, os valores associados desses membros de enumeração devem ser as potências de dois. Em seguida, você pode usar os [operadores lógicos de bit `|` ou `&` ](../operators/bitwise-and-shift-operators.md#enumeration-logical-operators) de opção para combinar opções ou combinações de interseção de opções, respectivamente. Para indicar que um tipo de enumeração declara campos de bits, aplique o atributo [flags](xref:System.FlagsAttribute) a ele. Como mostra o exemplo a seguir, você também pode incluir algumas combinações típicas na definição de um tipo de enumeração.

[!code-csharp[enum flags](snippets/shared/EnumType.cs#Flags)]

Para obter mais informações e exemplos, consulte a <xref:System.FlagsAttribute?displayProperty=nameWithType> página de referência da API e os [Membros não exclusivos e a seção de atributo flags](/dotnet/api/system.enum#non-exclusive-members-and-the-flags-attribute) da página de referência da <xref:System.Enum?displayProperty=nameWithType> API.

## <a name="the-systemenum-type-and-enum-constraint"></a>O tipo System. Enum e a restrição enum

O <xref:System.Enum?displayProperty=nameWithType> tipo é a classe base abstrata de todos os tipos de enumeração. Ele fornece vários métodos para obter informações sobre um tipo de enumeração e seus valores. Para obter mais informações e exemplos, consulte a <xref:System.Enum?displayProperty=nameWithType> página de referência da API.

A partir do C# 7,3, você pode usar `System.Enum` em uma restrição de classe base (que é conhecida como [restrição de enumeração](../../programming-guide/generics/constraints-on-type-parameters.md#enum-constraints)) para especificar que um parâmetro de tipo é um tipo de enumeração. Qualquer tipo de enumeração também satisfaz a `struct` restrição, que é usada para especificar que um parâmetro de tipo é um tipo de valor não anulável.

## <a name="conversions"></a>Conversões

Para qualquer tipo de enumeração, existem conversões explícitas entre o tipo de enumeração e seu tipo integral subjacente. Se você [converter](../operators/type-testing-and-cast.md#cast-expression) um valor de enumeração para seu tipo subjacente, o resultado será o valor integral associado de um membro de enumeração.

[!code-csharp[enum conversions](snippets/shared/EnumType.cs#Conversions)]

Use o <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> método para determinar se um tipo de enumeração contém um membro enum com determinado valor associado.

Para qualquer tipo de enumeração, existem conversões [boxing e unboxing](../../programming-guide/types/boxing-and-unboxing.md) de e para o <xref:System.Enum?displayProperty=nameWithType> tipo, respectivamente.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira as seguintes seções da [especificação da linguagem C#](~/_csharplang/spec/introduction.md):

- [Enumerações](~/_csharplang/spec/enums.md)
- [Operações e valores de enum](~/_csharplang/spec/enums.md#enum-values-and-operations)
- [Operadores lógicos de enumeração](~/_csharplang/spec/expressions.md#enumeration-logical-operators)
- [Operadores de comparação de enumeração](~/_csharplang/spec/expressions.md#enumeration-comparison-operators)
- [Conversões de enumeração explícitas](~/_csharplang/spec/conversions.md#explicit-enumeration-conversions)
- [Conversões implícitas de enumeração](~/_csharplang/spec/conversions.md#implicit-enumeration-conversions)

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Cadeias de caracteres de formato de enumeração](../../../standard/base-types/enumeration-format-strings.md)
- [Diretrizes de design-design de enumeração](../../../standard/design-guidelines/enum.md)
- [Diretrizes de design-convenções de nomenclatura de enumeração](../../../standard/design-guidelines/names-of-classes-structs-and-interfaces.md#naming-enumerations)
- [instrução switch](../keywords/switch.md)
