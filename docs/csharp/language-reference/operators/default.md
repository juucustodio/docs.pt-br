---
title: expressões de valor padrão-referência C#
description: Usar as expressões de valor padrão para obter o valor padrão de um tipo
ms.date: 03/13/2020
f1_keywords:
- default_CSharpKeyword
helpviewer_keywords:
- default keyword [C#]
ms.openlocfilehash: 92ad8e919567e1f9f57e6875d53c4055eb960829
ms.sourcegitcommit: e078b7540a8293ca1b604c9c0da1ff1506f0170b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91997650"
---
# <a name="default-value-expressions-c-reference"></a>expressões de valor padrão (referência C#)

Uma expressão de valor padrão produz o [valor padrão](../builtin-types/default-values.md) de um tipo. Há dois tipos de expressões de valor padrão: a chamada de [operador padrão](#default-operator) e um [literal padrão](#default-literal).

Você também usa a `default` palavra-chave como o rótulo de caso padrão dentro de uma [ `switch` instrução](../keywords/switch.md).

## <a name="default-operator"></a>operador default

O argumento do operador `default` deve ser o nome de um tipo ou um parâmetro de tipo, como mostra o exemplo a seguir:

[!code-csharp-interactive[default of T](snippets/shared/DefaultOperator.cs#WithOperand)]

## <a name="default-literal"></a>literal padrão

A partir do C# 7,1, você pode usar o literal `default` para produzir o valor padrão de um tipo quando o compilador pode inferir o tipo de expressão. A expressão literal `default` produz o mesmo valor que a expressão `default(T)`, em que `T` é o tipo inferido. Você pode usar o literal `default` em qualquer um dos seguintes casos:

- Na atribuição ou inicialização de uma variável.
- Na declaração do valor padrão para um parâmetro de [método opcional](../../methods.md#optional-parameters-and-arguments).
- Em uma chamada de método para fornecer um valor de argumento.
- Em uma [ `return` instrução](../keywords/return.md) ou como uma expressão em um [membro expression-apto para](../../programming-guide/statements-expressions-operators/expression-bodied-members.md).

O exemplo a seguir mostra o uso do literal `default`:

[!code-csharp-interactive[default literal](snippets/shared/DefaultOperator.cs#DefaultLiteral)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para saber mais, confira a seção [Expressões de valor padrão](~/_csharplang/spec/expressions.md#default-value-expressions) da [Especificação da linguagem C#](~/_csharplang/spec/introduction.md).

Para obter mais informações sobre o literal `default`, confira a [nota da proposta do recurso](~/_csharplang/proposals/csharp-7.1/target-typed-default.md).

## <a name="see-also"></a>Veja também

- [Referência de C#](../index.md)
- [Operadores e expressões C#](index.md)
- [Valores padrão de tipos C#](../builtin-types/default-values.md)
- [Generics in .NET (Genéricos no .NET)](../../../standard/generics/index.md)
