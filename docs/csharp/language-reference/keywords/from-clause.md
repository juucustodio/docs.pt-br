---
description: Cláusula from – Referência de C#
title: Cláusula from – Referência de C#
ms.date: 07/20/2015
f1_keywords:
- from_CSharpKeyword
- from
helpviewer_keywords:
- from clause [C#]
- from keyword [C#]
ms.assetid: 1aefd18c-1314-47f8-99ec-9bcefb09e699
ms.openlocfilehash: 474b22f5a9d8f12c8a4365159817f878761b563c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89140783"
---
# <a name="from-clause-c-reference"></a>Cláusula from (Referência de C#)

Uma expressão de consulta deve começar com uma cláusula `from`. Além disso, uma expressão de consulta pode conter subconsultas, que também começam com uma cláusula `from`. A cláusula `from` especifica o seguinte:

- A fonte de dados na qual a consulta ou subconsulta será executada.

- Uma *variável de intervalo* local que representa cada elemento na sequência de origem.

A variável de intervalo e a fonte de dados são fortemente tipadas. A fonte de dados referenciada na cláusula `from` deve ter um tipo de <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601> ou um tipo derivado, por exemplo, <xref:System.Linq.IQueryable%601>.

No exemplo a seguir, `numbers` é a fonte de dados e `num` é a variável de intervalo. Observe que ambas as variáveis são fortemente tipadas, mesmo com o uso da palavra-chave [var](var.md).

[!code-csharp[cscsrefQueryKeywords#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#1)]

## <a name="the-range-variable"></a>A variável de intervalo

O compilador infere que o tipo da variável de intervalo quando a fonte de dados implementa <xref:System.Collections.Generic.IEnumerable%601>. Por exemplo, se a fonte tem um tipo de `IEnumerable<Customer>`, então, a variável de intervalo será inferida como `Customer`. O tipo deve ser especificado explicitamente somente quando a fonte for um tipo `IEnumerable` não genérico, como <xref:System.Collections.ArrayList>. Para obter mais informações, consulte [como consultar uma ArrayList com LINQ](../../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md).

No exemplo anterior, `num` é inferido como do tipo `int`. Como a variável de intervalo é fortemente tipada, é possível chamar métodos nela ou usá-la em outras operações. Por exemplo, em vez de gravar `select num`, grave `select num.ToString()` para fazer com que a expressão de consulta retorne uma sequência de cadeias de caracteres em vez de números inteiros. Também é possível gravar `select num + 10` para fazer com que a expressão retorne a sequência 14, 11, 13, 12, 10. Para obter mais informações, consulte [cláusula SELECT](select-clause.md).

A variável de intervalo é como uma variável de iteração em uma instrução [foreach](foreach-in.md), com a exceção de uma diferença muito importante: na verdade, uma variável de intervalo nunca armazena dados da fonte. É apenas uma conveniência sintática que habilita a consulta a descrever o que ocorrerá quando ela for executada. Para obter mais informações, consulte [Introdução a Consultas de LINQ (C#)](../../programming-guide/concepts/linq/introduction-to-linq-queries.md).

## <a name="compound-from-clauses"></a>Cláusulas from compostas

Em alguns casos, cada elemento na sequência de origem pode ser uma sequência ou conter uma sequência. Por exemplo, a fonte de dados pode ser um `IEnumerable<Student>` em que cada objeto do aluno na sequência contenha uma lista de resultados de avaliações. Para acessar a lista interna dentro de cada elemento `Student`, use cláusulas compostas `from`. A técnica é parecida com o uso de instruções [foreach](foreach-in.md) aninhadas. É possível adicionar cláusulas [where](partial-method.md) ou [orderby](orderby-clause.md) a qualquer cláusula `from` para filtrar os resultados. O exemplo a seguir mostra uma sequência de objetos `Student`, em cada um contém uma `List` interna de inteiros que representam de resultados de avaliações. Para acessar a lista interna, use uma cláusula composta `from`. É possível inserir cláusulas entre as duas cláusulas `from`, se necessário.

[!code-csharp[cscsrefQueryKeywords#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#2)]

## <a name="using-multiple-from-clauses-to-perform-joins"></a>Usando Várias Cláusulas from para Realizar Uniões

Uma cláusula composta `from` é usada para acessar coleções internas em uma fonte de dados única. No entanto, uma consulta também pode conter várias cláusulas `from` que geram consultas complementares de fontes de dados independentes. Essa técnica habilita a execução de determinados tipos de operações de união que não são possíveis por meio da [cláusula join](join-clause.md).

A exemplo a seguir mostra como duas cláusulas `from` podem ser usadas para formar uma união cruzada completa de duas fontes de dados.

[!code-csharp[cscsrefQueryKeywords#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#3)]

Para obter mais informações sobre as operações de união que usam várias cláusulas `from`, consulte [Executar junções externas esquerdas](../../linq/perform-left-outer-joins.md).

## <a name="see-also"></a>Confira também

- [Palavras-chave de consulta (LINQ)](query-keywords.md)
- [LINQ (Consulta Integrada à Linguagem)](../../linq/index.md)
