---
description: Cláusula where – Referência de C#
title: Cláusula where – Referência de C#
ms.date: 07/20/2015
f1_keywords:
- whereclause_CSharpKeyword
helpviewer_keywords:
- where keyword [C#]
- where clause [C#]
ms.assetid: 7f9bf952-7744-4f91-b676-cddb55d107c3
ms.openlocfilehash: 58a8dc226bb2720b6a8251f028712a80f74e893c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89141680"
---
# <a name="where-clause-c-reference"></a>Cláusula where (Referência de C#)

A cláusula `where` é usada em uma expressão de consulta para especificar quais elementos da fonte de dados serão retornados na expressão de consulta. Aplica-se uma condição booliana (*predicate*) para cada elemento de origem (referenciado pela variável de intervalo) e retorna aqueles para os quais a condição especificada for verdadeira. Uma única expressão de consulta pode conter várias cláusulas `where` e uma única cláusula pode conter várias subexpressões de predicado.

## <a name="example"></a>Exemplo

No exemplo a seguir, a cláusula `where` filtra todos os números, exceto aqueles que são menores que cinco. Se você remover a cláusula `where`, todos os números da fonte de dados serão retornados. A expressão `num < 5` é o predicado aplicado a cada elemento.

[!code-csharp[cscsrefQueryKeywords#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Where.cs#5)]

## <a name="example"></a>Exemplo

Em uma única `where` cláusula, você pode especificar quantos predicados forem necessários usando os [&&](../operators/boolean-logical-operators.md#conditional-logical-and-operator-) operadores e [&#124;&#124;](../operators/boolean-logical-operators.md#conditional-logical-or-operator-) . No exemplo a seguir, a consulta especifica dois predicados para selecionar apenas os números pares que são menores que cinco.

[!code-csharp[cscsrefQueryKeywords#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Where.cs#6)]  

## <a name="example"></a>Exemplo

Uma cláusula `where` pode conter um ou mais métodos que retornam valores boolianos. No exemplo a seguir, a cláusula `where` usa um método para determinar se o valor atual da variável de intervalo é par ou ímpar.

[!code-csharp[cscsrefQueryKeywords#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Where.cs#7)]

## <a name="remarks"></a>Comentários

A cláusula `where` é um mecanismo de filtragem. Ela pode ser posicionada em quase qualquer lugar em uma expressão de consulta, exceto que ela não pode ser a primeira ou a última cláusula. A cláusula `where` pode aparecer antes ou depois de uma cláusula [group](group-clause.md) dependendo se você tiver que filtrar os elementos de origem antes ou depois de eles serem agrupados.

Se um predicado especificado não for válido para os elementos na fonte de dados, o resultado será um erro em tempo de compilação. Esse é um dos benefícios da verificação de tipo forte fornecida pelo LINQ.

Em tempo de compilação, a palavra-chave `where` é convertida em uma chamada para o método de operador de consulta padrão <xref:System.Linq.Enumerable.Where%2A>.

## <a name="see-also"></a>Confira também

- [Palavras-chave de consulta (LINQ)](query-keywords.md)
- [Cláusula from](from-clause.md)
- [cláusula SELECT](select-clause.md)
- [Filtrar dados](../../programming-guide/concepts/linq/filtering-data.md)
- [LINQ em C#](../../linq/index.md)
- [LINQ (Consulta Integrada à Linguagem)](../../programming-guide/concepts/linq/index.md)
