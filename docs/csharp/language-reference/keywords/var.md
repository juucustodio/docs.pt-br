---
description: referência de var-C#
title: referência de var-C#
ms.date: 10/02/2020
f1_keywords:
- var
- var_CSharpKeyword
helpviewer_keywords:
- var keyword [C#]
ms.assetid: 0777850a-2691-4e3e-927f-0c850f5efe15
ms.openlocfilehash: d04bea9bcf5be726d3e81a1a53abed31f59330a0
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91608706"
---
# <a name="var-c-reference"></a>var (referência C#)

Começando com o C# 3, as variáveis que são declaradas no escopo do método podem ter um "tipo" implícito `var` . Uma variável local de tipo implícito é fortemente tipada, como se você mesmo tivesse declarado o tipo, mas o compilador determina o tipo. As duas declarações a seguir de `i` são funcionalmente equivalentes:

```csharp
var i = 10; // Implicitly typed.
int i = 10; // Explicitly typed.
```

> [!IMPORTANT]
> Quando `var` é usado com [tipos de referência anuláveis](../builtin-types/nullable-reference-types.md) habilitados, ele sempre implica um tipo de referência anulável mesmo que o tipo de expressão não seja anulável.

Um uso comum da `var` palavra-chave é com expressões de invocação de construtor. O uso de `var` permite que você não repita um nome de tipo em uma declaração de variável e instanciação de objeto, como mostra o exemplo a seguir:

```csharp
var xs = new List<int>();
```

A partir do C# 9,0, você pode usar uma [ `new` expressão](../operators/new-operator.md) de tipo de destino como alternativa:

```csharp
List<int> xs = new();
List<int>? ys = new();
```

## <a name="example"></a>Exemplo

O exemplo a seguir mostra duas expressões de consulta. Na primeira expressão, o uso de `var` é permitido, mas não é necessário, pois o tipo do resultado da consulta pode ser declarado explicitamente como um `IEnumerable<string>`. No entanto, na segunda expressão, `var` permite que o resultado seja uma coleção de tipos anônimos e o nome desse tipo não é acessível, exceto para o próprio compilador. O uso de `var` elimina a necessidade de criar uma nova classe para o resultado. Observe que no exemplo 2, a variável de iteração `foreach``item` também deve ser implicitamente tipada.

[!code-csharp[csrefKeywordsTypes#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#18)]

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Variáveis locais digitadas implicitamente](../../programming-guide/classes-and-structs/implicitly-typed-local-variables.md)
- [Relações de tipo em operações de consulta LINQ](../../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)
