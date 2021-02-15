---
title: Tipos de valor anulável-referência C#
description: Saiba mais sobre os tipos de valor nulos do C# e como usá-los
ms.date: 11/04/2019
helpviewer_keywords:
- nullable value types [C#]
ms.openlocfilehash: 3ab2dff6b7399b0458a69d4498b2ebda24f6c5cc
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471829"
---
# <a name="nullable-value-types-c-reference"></a>Tipos de valores anuláveis (referência C#)

Um *tipo de valor anulável* `T?` representa todos os valores de seu [tipo de valor](value-types.md) subjacente `T` e um valor [nulo](../keywords/null.md) adicional. Por exemplo, você pode atribuir qualquer um dos três valores a seguir a uma `bool?` variável: `true` , `false` ou `null` . Um tipo de valor subjacente `T` não pode ser um tipo de valor anulável em si.

> [!NOTE]
> O C# 8,0 apresenta o recurso de tipos de referência anulável. Para obter mais informações, consulte [tipos de referência anuláveis](nullable-reference-types.md). Os tipos de valor anulável estão disponíveis a partir do C# 2.

Qualquer tipo de valor anulável é uma instância da <xref:System.Nullable%601?displayProperty=nameWithType> estrutura genérica. Você pode se referir a um tipo de valor anulável com um tipo subjacente `T` em qualquer um dos seguintes formulários intercambiáveis: `Nullable<T>` ou `T?` .

Normalmente, você usa um tipo de valor anulável quando precisa representar o valor indefinido de um tipo de valor subjacente. Por exemplo, um booliano ou `bool` variável pode ser apenas `true` ou `false` . No entanto, em alguns aplicativos, um valor de variável pode ser indefinido ou estar ausente. Por exemplo, um campo de banco de dados pode conter `true` ou ou `false` não pode conter nenhum valor, ou seja, `NULL` . Você pode usar o `bool?` tipo nesse cenário.

## <a name="declaration-and-assignment"></a>Declaração e atribuição

Como um tipo de valor é implicitamente conversível para o tipo de valor anulável correspondente, você pode atribuir um valor a uma variável de um tipo de valor anulável, como faria com o tipo de valor subjacente. Você também pode atribuir o `null` valor. Por exemplo:

[!code-csharp[declare and assign](snippets/shared/NullableValueTypes.cs#Declaration)]

O valor padrão de um tipo de valor anulável representa `null` , ou seja, é uma instância cuja <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> propriedade retorna `false` .

## <a name="examination-of-an-instance-of-a-nullable-value-type"></a>Exame de uma instância de um tipo de valor anulável

A partir do C# 7,0, você pode usar o [ `is` operador com um padrão de tipo](../operators/type-testing-and-cast.md#type-testing-with-pattern-matching) para examinar uma instância de um tipo de valor anulável para `null` e recuperar um valor de um tipo subjacente:

[!code-csharp-interactive[use pattern matching](snippets/shared/NullableValueTypes.cs#PatternMatching)]

Você sempre pode usar as seguintes propriedades somente leitura para examinar e obter um valor de uma variável de tipo de valor anulável:

- <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> indica se uma instância de um tipo de valor anulável tem um valor de seu tipo subjacente.

- <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> obtém o valor de um tipo subjacente quando <xref:System.Nullable%601.HasValue%2A> é `true`. Quando <xref:System.Nullable%601.HasValue%2A> é `false`, a propriedade <xref:System.Nullable%601.Value%2A> gera uma <xref:System.InvalidOperationException>.

O exemplo a seguir usa a `HasValue` propriedade para testar se a variável contém um valor antes de exibi-la:

[!code-csharp-interactive[use HasValue](snippets/shared/NullableValueTypes.cs#HasValue)]

Você também pode comparar uma variável de um tipo de valor anulável com `null` em vez de usar a `HasValue` propriedade, como mostra o exemplo a seguir:

[!code-csharp-interactive[use comparison with null](snippets/shared/NullableValueTypes.cs#CompareWithNull)]

## <a name="conversion-from-a-nullable-value-type-to-an-underlying-type"></a>Conversão de um tipo de valor anulável para um tipo subjacente

Se você quiser atribuir um valor de tipo de valor anulável a uma variável de tipo de valor não anulável, talvez seja necessário especificar o valor a ser atribuído no lugar de `null` . Use o [operador `??` de União nulo](../operators/null-coalescing-operator.md) para fazer isso (você também pode usar o <xref:System.Nullable%601.GetValueOrDefault(%600)?displayProperty=nameWithType> método para a mesma finalidade):

[!code-csharp-interactive[?? operator](snippets/shared/NullableValueTypes.cs#NullCoalescing)]

Se você quiser usar o valor [padrão](default-values.md) do tipo de valor subjacente no lugar de `null` , use o <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> método.

Você também pode converter explicitamente um tipo de valor anulável para um tipo não anulável, como mostra o exemplo a seguir:

[!code-csharp[explicit cast](snippets/shared/NullableValueTypes.cs#Cast)]

Em tempo de execução, se o valor de um tipo de valor anulável for `null` , a conversão explícita lançará um <xref:System.InvalidOperationException> .

Um tipo de valor não anulável `T` é implicitamente conversível para o tipo de valor anulável correspondente `T?` .

## <a name="lifted-operators"></a>Operadores levantados

Os [operadores](../operators/index.md) unários e binários predefinidos ou quaisquer operadores sobrecarregados com suporte de um tipo de valor `T` também têm suporte pelo tipo de valor anulável correspondente `T?` . Esses operadores, também conhecidos como *operadores levantados*, produzem `null` se um ou ambos os operandos são `null` ; caso contrário, o operador usa os valores contidos de seus operandos para calcular o resultado. Por exemplo:

[!code-csharp[lifted operators](snippets/shared/NullableValueTypes.cs#LiftedOperator)]

> [!NOTE]
> Para o `bool?` tipo, os operadores e predefinidos `&` `|` não seguem as regras descritas nesta seção: o resultado de uma avaliação de operador pode ser não nulo mesmo que um dos operandos seja `null` . Para obter mais informações, confira a seção [Operadores lógicos booleanos anuláveis](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators) do artigo [Operadores lógicos boolianos](../operators/boolean-logical-operators.md).

Para os [operadores de comparação](../operators/comparison-operators.md) `<` , `>` , `<=` e `>=` , se um ou ambos os operandos forem `null` , o resultado será `false` ; caso contrário, os valores contidos dos operandos serão comparados. Não presuma que como uma comparação (por exemplo, `<=`) retorna `false`, a comparação oposta (`>`) retorna `true`. O exemplo a seguir mostra que 10

- Nem maior ou igual a `null`
- Nem menor que `null`

[!code-csharp-interactive[relational and equality operators](snippets/shared/NullableValueTypes.cs#ComparisonOperators)]

Para o [operador de igualdade](../operators/equality-operators.md#equality-operator-) `==` , se ambos os operandos forem `null` , o resultado será `true` , se apenas um dos operandos for `null` , o resultado será `false` ; caso contrário, os valores contidos dos operandos serão comparados.

Para o [operador de desigualdade](../operators/equality-operators.md#inequality-operator-) `!=` , se ambos os operandos forem `null` , o resultado será `false` , se apenas um dos operandos for `null` , o resultado será `true` ; caso contrário, os valores contidos dos operandos serão comparados.

Se existir uma [conversão definida pelo usuário](../operators/user-defined-conversion-operators.md) entre dois tipos de valor, a mesma conversão também poderá ser usada entre os tipos de valores anuláveis correspondentes.

## <a name="boxing-and-unboxing"></a>Conversão boxing e unboxing

Uma instância de um tipo de valor Anulável `T?` é [in a box](../../programming-guide/types/boxing-and-unboxing.md) da seguinte maneira:

- Se <xref:System.Nullable%601.HasValue%2A> retorna `false`, a referência nula é produzida.
- Se <xref:System.Nullable%601.HasValue%2A> retorna `true` , o valor correspondente do tipo de valor subjacente `T` é Box, não a instância de <xref:System.Nullable%601> .

Você pode unbox um valor em caixa de um tipo de valor `T` para o tipo de valor anulável correspondente `T?` , como mostra o exemplo a seguir:

[!code-csharp-interactive[boxing and unboxing](snippets/shared/NullableValueTypes.cs#Boxing)]

## <a name="how-to-identify-a-nullable-value-type"></a>Como identificar um tipo de valor anulável

O exemplo a seguir mostra como determinar se uma <xref:System.Type?displayProperty=nameWithType> instância representa um tipo de valor anulável construído, ou seja, o <xref:System.Nullable%601?displayProperty=nameWithType> tipo com um parâmetro de tipo especificado `T` :

[!code-csharp-interactive[whether Type is nullable](snippets/shared/NullableValueTypes.cs#IsTypeNullable)]

Como mostra o exemplo, você usa o operador [typeof](../operators/type-testing-and-cast.md#typeof-operator) para criar uma <xref:System.Type?displayProperty=nameWithType> instância.

Se você quiser determinar se uma instância é de um tipo de valor anulável, não use o <xref:System.Object.GetType%2A?displayProperty=nameWithType> método para obter uma <xref:System.Type> instância a ser testada com o código anterior. Quando você chama o <xref:System.Object.GetType%2A?displayProperty=nameWithType> método em uma instância de um tipo de valor anulável, a instância é [encaixada](#boxing-and-unboxing) no <xref:System.Object> . Como Boxing de uma instância não nula de um tipo de valor anulável é equivalente à Boxing de um valor do tipo subjacente, <xref:System.Object.GetType%2A> retorna uma <xref:System.Type> instância que representa o tipo subjacente de um tipo de valor anulável:

[!code-csharp-interactive[GetType example](snippets/shared/NullableValueTypes.cs#GetType)]

Além disso, não use o operador [is](../operators/type-testing-and-cast.md#is-operator) para determinar se uma instância é de um tipo de valor anulável. Como mostra o exemplo a seguir, você não pode distinguir tipos de uma instância de tipo de valor anulável e sua instância de tipo subjacente com o `is` operador:

[!code-csharp-interactive[is operator example](snippets/shared/NullableValueTypes.cs#IsOperator)]

Você pode usar o código apresentado no exemplo a seguir para determinar se uma instância é de um tipo de valor anulável:

[!code-csharp-interactive[whether an instance is of a nullable type](snippets/shared/NullableValueTypes.cs#IsInstanceNullable)]

> [!NOTE]
> Os métodos descritos nesta seção não são aplicáveis no caso de tipos de [referência anuláveis](nullable-reference-types.md).

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira as seguintes seções da [especificação da linguagem C#](~/_csharplang/spec/introduction.md):

- [Tipos anuláveis](~/_csharplang/spec/types.md#nullable-types)
- [Operadores levantados](~/_csharplang/spec/expressions.md#lifted-operators)
- [Conversões anuláveis implícitas](~/_csharplang/spec/conversions.md#implicit-nullable-conversions)
- [Conversões anuláveis explícitas](~/_csharplang/spec/conversions.md#explicit-nullable-conversions)
- [Operadores de conversão levantados](~/_csharplang/spec/conversions.md#lifted-conversion-operators)

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [O que exatamente "levantado" significa?](/archive/blogs/ericlippert/what-exactly-does-lifted-mean)
- <xref:System.Nullable%601?displayProperty=nameWithType>
- <xref:System.Nullable?displayProperty=nameWithType>
- <xref:System.Nullable.GetUnderlyingType%2A?displayProperty=nameWithType>
- [Tipos de referência anuláveis](nullable-reference-types.md)
