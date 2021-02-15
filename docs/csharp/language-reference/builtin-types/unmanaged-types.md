---
description: 'Saiba mais sobre os tipos não gerenciados em C #'
title: Tipos não gerenciados – referência em C#
ms.date: 09/06/2019
helpviewer_keywords:
- unmanaged type [C#]
ms.openlocfilehash: 4374872af13c94e1a1af6b9f2c431f076c6f7dff
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471793"
---
# <a name="unmanaged-types-c-reference"></a>Tipos não gerenciados (referência em C#)

Um tipo é um **tipo não gerenciado** , se for qualquer um dos seguintes tipos:

- `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal` ou `bool`
- Qualquer tipo de [Enumeração](enum.md)
- Qualquer tipo de [ponteiro](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- Qualquer tipo de [struct](struct.md) definido pelo usuário que contém campos de tipos não gerenciados somente e, em C# 7,3 e anterior, não é um tipo construído (um tipo que inclui pelo menos um argumento de tipo)

A partir do C# 7,3, você pode usar a [ `unmanaged` restrição](../../programming-guide/generics/constraints-on-type-parameters.md#unmanaged-constraint) para especificar que um parâmetro de tipo é um tipo não gerenciado não-ponteiro e não anulável.

A partir do C# 8,0, um tipo struct *construído* que contém campos de tipos não gerenciados também é não gerenciado, como mostra o exemplo a seguir:

[!code-csharp[unmanaged constructed types](snippets/shared/UnmanagedTypes.cs#ProgramExample)]

Uma estrutura genérica pode ser a fonte de tipos construídos não gerenciados e não gerenciados. O exemplo anterior define uma struct genérica `Coords<T>` e apresenta os exemplos de tipos construídos não gerenciados. O exemplo de não é um tipo não gerenciado `Coords<object>` . Não é não gerenciado porque tem os campos do `object` tipo, que não são gerenciados. Se você quiser que *todos os* tipos construídos sejam tipos não gerenciados, use a `unmanaged` restrição na definição de uma estrutura genérica:

[!code-csharp[unmanaged constraint in type definition](snippets/shared/UnmanagedTypes.cs#AlwaysUnmanaged)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para saber mais, confira a seção [Tipos de ponteiro](~/_csharplang/spec/unsafe-code.md#pointer-types) na [Especificação da linguagem C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Tipos de ponteiro](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [Tipos relacionados a memória e extensão](../../../standard/memory-and-spans/index.md)
- [Operador sizeof](../operators/sizeof.md)
- [stackalloc](../operators/stackalloc.md)
