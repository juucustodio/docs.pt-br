---
description: operador new – Referência em C#
title: operador new – Referência em C#
ms.date: 10/02/2020
f1_keywords:
- new_CSharpKeyword
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: 3125f3d2c694dcfc5682ee482f3f76072ac3726d
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91609376"
---
# <a name="new-operator-c-reference"></a>operador new (Referência em C#)

O operador `new` cria uma nova instância de um tipo.

Você também pode usar a palavra-chave `new` como um [modificador de declaração de membro](../keywords/new-modifier.md) ou uma [restrição de tipo genérico](../keywords/new-constraint.md).

## <a name="constructor-invocation"></a>Chamada de construtor

Para criar uma nova instância de um tipo, você normalmente invoca um dos [construtores](../../programming-guide/classes-and-structs/constructors.md) desse tipo usando o operador `new`:

[!code-csharp-interactive[invoke constructor](snippets/shared/NewOperator.cs#Constructor)]

Você pode usar um [inicializador de objeto ou coleção](../../programming-guide/classes-and-structs/object-and-collection-initializers.md) com o operador `new` para instanciar e inicializar um objeto em uma instrução, como mostra o exemplo a seguir:

[!code-csharp-interactive[constructor with initializer](snippets/shared/NewOperator.cs#ConstructorWithInitializer)]

A partir do C# 9,0, as expressões de invocação de Construtor são de tipo de destino. Ou seja, se um tipo de destino de uma expressão for conhecido, você poderá omitir um nome de tipo, como mostra o exemplo a seguir:

:::code language="csharp" source="snippets/shared/NewOperator.cs" id="SnippetTargetTyped":::

Como mostra o exemplo anterior, você sempre usa parênteses em uma expressão de tipo de destino `new` .

Se um tipo de destino de uma `new` expressão for desconhecido (por exemplo, ao usar a [`var`](../keywords/var.md) palavra-chave), você deverá especificar um nome de tipo.

## <a name="array-creation"></a>Criação de matriz

Você também usar o operador `new` para criar uma instância de matriz, como mostra o exemplo a seguir:

[!code-csharp-interactive[create array](snippets/shared/NewOperator.cs#Array)]

Use a sintaxe de inicialização de matriz para criar uma instância de matriz e preenchê-la com os elementos em uma instrução. O exemplo a seguir mostra várias maneiras de como fazer isso:

[!code-csharp-interactive[initialize array](snippets/shared/NewOperator.cs#ArrayInitialization)]

Para obter mais informações sobre matrizes, confira [Matrizes](../../programming-guide/arrays/index.md).

## <a name="instantiation-of-anonymous-types"></a>Instanciação de tipos anônimos

Para criar uma instância de um [tipo anônimo](../../programming-guide/classes-and-structs/anonymous-types.md), use o operador `new` e a sintaxe do inicializador de objeto:

[!code-csharp-interactive[anonymous type](snippets/shared/NewOperator.cs#AnonymousType)]

## <a name="destruction-of-type-instances"></a>Destruição de instâncias do tipo

Você não precisa destruir as instâncias do tipo criadas anteriormente. As instâncias dos tipos de referência e de valor são destruídas automaticamente. As instâncias dos tipos de valor serão destruídas assim que o contexto que as contém for destruído. Instâncias de tipos de referência são destruídas pelo [coletor de lixo](../../../standard/garbage-collection/index.md) em algum momento não especificado depois que a última referência a eles é removida.

Para instâncias de tipo que contêm recursos não gerenciados, por exemplo, um identificador de arquivo, é recomendável empregar uma limpeza determinística para garantir que os recursos que eles contêm sejam liberados assim que possível. Para obter mais informações, veja o artigo <xref:System.IDisposable?displayProperty=nameWithType> Referência da API e a [instrução de uso](../keywords/using-statement.md).

## <a name="operator-overloadability"></a>Capacidade de sobrecarga do operador

Um tipo definido pelo usuário não pode sobrecarregar o operador `new`.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para saber mais, confira a seção [O operador new](~/_csharplang/spec/expressions.md#the-new-operator) na [especificação da linguagem C#](~/_csharplang/spec/introduction.md).

Para obter mais informações sobre uma expressão de tipo de destino `new` , consulte a [Nota de proposta de recurso](~/_csharplang/proposals/csharp-9.0/target-typed-new.md).

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Operadores e expressões C#](index.md)
- [Inicializadores de objeto e coleção](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)
