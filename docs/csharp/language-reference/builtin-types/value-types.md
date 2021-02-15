---
description: 'Saiba mais sobre tipos de valor, seus tipos e os internos em C #'
title: Tipos de valor-referência C#
ms.date: 01/22/2020
f1_keywords:
- cs.valuetypes
helpviewer_keywords:
- value types [C#]
- types [C#], value types
- C# language, value types
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
ms.openlocfilehash: 64c9e9eba2495531cfef8a603d53fb21c95c87a4
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599389"
---
# <a name="value-types-c-reference"></a>Tipos de valor (referência C#)

Tipos de *valor* e [tipos de referência](../keywords/reference-types.md) são as duas principais categorias de tipos C#. Uma variável de um tipo Value contém uma instância do tipo. Isso é diferente de uma variável de um tipo de referência, que contém uma referência a uma instância do tipo. Por padrão, na [atribuição](../operators/assignment-operator.md), passando um argumento para um método e retornando um resultado de método, valores de variáveis são copiados. No caso de variáveis de tipo de valor, as instâncias de tipo correspondentes são copiadas. O exemplo a seguir demonstra esse comportamento:

[!code-csharp[copy of values](snippets/shared/ValueTypes.cs#ValueTypeCopied)]

Como mostra o exemplo anterior, as operações em uma variável de tipo de valor afetam apenas essa instância do tipo de valor, armazenado na variável.

Se um tipo de valor contiver um membro de dados de um tipo de referência, somente a referência à instância do tipo de referência será copiada quando uma instância de tipo de valor for copiada. A instância de tipo de valor de cópia e original tem acesso à mesma instância de tipo de referência. O exemplo a seguir demonstra esse comportamento:

[!code-csharp[shallow copy](snippets/shared/ValueTypes.cs#ShallowCopy)]

> [!NOTE]
> Para tornar seu código menos propenso a erros e mais robusto, defina e use tipos de valor imutável. Este artigo usa tipos de valores mutáveis somente para fins de demonstração.

## <a name="kinds-of-value-types-and-type-constraints"></a>Tipos de tipos de valor e restrições de tipo

Um tipo de valor pode ser um dos dois tipos a seguir:

- um [tipo de estrutura](struct.md), que encapsula dados e funcionalidade relacionada
- um [tipo de enumeração](enum.md), que é definido por um conjunto de constantes nomeadas e representa uma opção ou uma combinação de opções

Um [tipo de valor anulável](nullable-value-types.md) `T?` representa todos os valores de seu tipo de valor subjacente `T` e um valor [nulo](../keywords/null.md) adicional. Não é possível atribuir `null` a uma variável de um tipo de valor, a menos que seja um tipo de valor anulável.

Você pode usar a [ `struct` restrição](../../programming-guide/generics/constraints-on-type-parameters.md) para especificar que um parâmetro de tipo é um tipo de valor não anulável. Os tipos de estrutura e enumeração atendem à `struct` restrição. A partir do C# 7,3, você pode usar `System.Enum` em uma restrição de classe base (que é conhecida como [restrição de enumeração](../../programming-guide/generics/constraints-on-type-parameters.md#enum-constraints)) para especificar que um parâmetro de tipo é um tipo de enumeração.

## <a name="built-in-value-types"></a>Tipos de valores internos

O C# fornece os seguintes tipos de valor internos, também conhecidos como *tipos simples*:

- [Tipos numéricos integrais](integral-numeric-types.md)
- [Tipos numéricos de ponto flutuante](floating-point-numeric-types.md)
- [bool](bool.md) que representa um valor booliano
- [Char](char.md) que representa um caractere Unicode UTF-16

Todos os tipos simples são tipos de estrutura e diferem de outros tipos de estrutura, pois permitem determinadas operações adicionais:

- Você pode usar literais para fornecer um valor de um tipo simples. Por exemplo, `'A'` é um literal do tipo `char` e `2001` é um literal do tipo `int`.

- Você pode declarar constantes dos tipos simples com a palavra-chave [const](../keywords/const.md). Não é possível ter constantes de outros tipos de estrutura.

- Expressões constantes, cujos operandos são todas constantes dos tipos simples, são avaliadas no momento da compilação.

A partir do C# 7,0, o C# dá suporte a [tuplas de valor](value-tuples.md). Uma tupla de valor é um tipo de valor, mas não um tipo simples.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira as seguintes seções da [especificação da linguagem C#](~/_csharplang/spec/introduction.md):

- [Tipos de valor](~/_csharplang/spec/types.md#value-types)
- [Tipos simples](~/_csharplang/spec/types.md#simple-types)
- [Variáveis](~/_csharplang/spec/variables.md)

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- <xref:System.ValueType?displayProperty=nameWithType>
- [Tipos de referência](../keywords/reference-types.md)
