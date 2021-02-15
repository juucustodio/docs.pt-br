---
description: 'Operador ?: – referência do C#'
title: 'Operador ?: – referência do C#'
ms.date: 09/17/2020
f1_keywords:
- ?:_CSharpKeyword
- ?_CSharpKeyword
- :_CSharpKeyword
helpviewer_keywords:
- '?: operator [C#]'
- conditional operator (?:) [C#]
ms.assetid: e83a17f1-7500-48ba-8bee-2fbc4c847af4
ms.openlocfilehash: b6add045983619169bed0cd9f32eb27dba0a0338
ms.sourcegitcommit: a8730298170b8d96b4272e0c3dfc9819c606947b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2020
ms.locfileid: "90738873"
---
# <a name="-operator-c-reference"></a>Operador ?: (referência do C#)

O operador condicional `?:` , também conhecido como operador condicional Ternário, avalia uma expressão booliana e retorna o resultado de uma das duas expressões, dependendo se a expressão booliana é avaliada como `true` ou `false` .

A sintaxe do operador condicional é a seguinte:

```csharp
condition ? consequent : alternative
```

A expressão `condition` deve ser avaliada para `true` ou `false`. Se `condition` for avaliada como `true`, a expressão `consequent` será avaliada e seu resultado se tornará o resultado da operação. Se `condition` for avaliada como `false`, a expressão `alternative` será avaliada e seu resultado se tornará o resultado da operação. Somente `consequent` ou `alternative` é avaliada.

A partir do C# 9,0, as expressões condicionais são de tipo de destino. Ou seja, se um tipo de destino de uma expressão condicional for conhecido, os tipos de `consequent` e `alternative` deverão ser conversíveis implicitamente para o tipo de destino, como mostra o exemplo a seguir:

[!code-csharp[target-typed conditional](snippets/shared/ConditionalOperator.cs#TargetTyped)]

Se um tipo de destino de uma expressão condicional for desconhecido (por exemplo, quando você usar a [`var`](../keywords/var.md) palavra-chave) ou em C# 8,0 e anterior, o tipo de `consequent` e `alternative` deverá ser o mesmo ou deve haver uma conversão implícita de um tipo para o outro:

[!code-csharp[not target-typed conditional](snippets/shared/ConditionalOperator.cs#NotTargetTyped)]

O operador condicional é associativo direito, ou seja, uma expressão da forma

```csharp
a ? b : c ? d : e
```

é avaliada como

```csharp
a ? b : (c ? d : e)
```

> [!TIP]
> Você pode usar o seguinte dispositivo mnemônico para se lembrar de como o operador condicional é avaliado:
>
> ```text
> is this condition true ? yes : no
> ```

O exemplo a seguir demonstra o uso do operador condicional:

[!code-csharp-interactive[non ref conditional](snippets/shared/ConditionalOperator.cs#ConditionalValue)]

## <a name="conditional-ref-expression"></a>Expressão condicional ref

A partir do C# 7,2, uma variável local [ref local](../keywords/ref.md#ref-locals) ou [ref ReadOnly](../keywords/ref.md#ref-readonly-locals) pode ser atribuída condicionalmente com uma expressão ref condicional. Você também pode usar uma expressão ref condicional como um [valor de retorno de referência](../keywords/ref.md#reference-return-values) ou como um [ `ref` argumento de método](../keywords/ref.md#passing-an-argument-by-reference).

A sintaxe de uma expressão ref condicional é a seguinte:

```csharp
condition ? ref consequent : ref alternative
```

Assim como o operador condicional original, uma expressão ref condicional avalia apenas uma das duas expressões: `consequent` ou `alternative` .

No caso de uma expressão ref condicional, o tipo de `consequent` e `alternative` deve ser o mesmo. As expressões de referência condicional não são de tipo alvo.

O exemplo a seguir demonstra o uso de uma expressão de referência condicional:

[!code-csharp-interactive[conditional ref](snippets/shared/ConditionalOperator.cs#ConditionalRef)]

## <a name="conditional-operator-and-an-ifelse-statement"></a>Operador condicional e uma instrução `if..else`

O uso do operador condicional em vez de uma instrução [If-Else](../keywords/if-else.md) pode resultar em um código mais conciso em casos em que você precisa de uma condição para computar um valor. O exemplo a seguir demonstra duas maneiras de classificar um inteiro como negativo ou não negativo:

[!code-csharp[conditional and if-else](snippets/shared/ConditionalOperator.cs#CompareWithIf)]

## <a name="operator-overloadability"></a>Capacidade de sobrecarga do operador

Um tipo definido pelo usuário não pode sobrecarregar o operador condicional.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para saber mais, confira a seção [Operador condicional](~/_csharplang/spec/expressions.md#conditional-operator) na [especificação da linguagem C#](~/_csharplang/spec/introduction.md).

Para obter mais informações sobre os recursos adicionados em C# 7,2 e posterior, consulte as seguintes notas de proposta de recurso:

- [Expressões de referência condicional (C# 7,2)](~/_csharplang/proposals/csharp-7.2/conditional-ref.md)
- [Expressão condicional de tipo de destino (C# 9,0)](~/_csharplang/proposals/csharp-9.0/target-typed-conditional-expression.md)

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Operadores e expressões C#](index.md)
- [Instrução if-else](../keywords/if-else.md)
- [Operadores ?. e ?[]](member-access-operators.md#null-conditional-operators--and-)
- [?? e?? = operadores](null-coalescing-operator.md)
- [ref keyword](../keywords/ref.md)
