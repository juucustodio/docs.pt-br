---
description: Cláusula group – Referência de C#
title: Cláusula group – Referência de C#
ms.date: 07/20/2015
f1_keywords:
- group
- group_CSharpKeyword
helpviewer_keywords:
- group keyword [C#]
- group clause [C#]
ms.assetid: c817242e-b12c-4baa-a57e-73ee138f34d1
ms.openlocfilehash: 5e642492b4b36bb0464baf16baa80c58c19ba9f1
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89138222"
---
# <a name="group-clause-c-reference"></a>Cláusula group (Referência de C#)

A cláusula `group` retorna uma sequência de objetos <xref:System.Linq.IGrouping%602> que contêm zero ou mais itens que correspondem ao valor de chave do grupo. Por exemplo, é possível agrupar uma sequência de cadeias de caracteres de acordo com a primeira letra de cada cadeia de caracteres. Nesse caso, a primeira letra é a chave, tem um tipo [char](../builtin-types/char.md) e é armazenada na propriedade `Key` de cada objeto <xref:System.Linq.IGrouping%602>. O compilador infere o tipo da chave.

É possível finalizar uma expressão de consulta com uma cláusula `group`, conforme mostrado no exemplo a seguir:

[!code-csharp[cscsrefQueryKeywords#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#10)]

Caso deseje executar mais operações de consulta em cada grupo, é possível especificar um identificador temporário usando a palavra-chave contextual [into](into.md). Ao usar `into`, é necessário continuar a consulta e, em algum momento, finalizá-la com uma instrução `select` ou outra cláusula `group`, conforme mostrado no trecho a seguir:

[!code-csharp[cscsrefQueryKeywords#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#11)]

Exemplos mais completos do uso de `group` com e sem `into` serão apresentados na seção Exemplo deste artigo.

## <a name="enumerating-the-results-of-a-group-query"></a>Enumerando os resultados de uma consulta de grupo

Como os objetos <xref:System.Linq.IGrouping%602> produzidos por uma consulta `group` são essencialmente uma lista de listas, você deve usar um loop aninhado [foreach](foreach-in.md) para acessar os itens em cada grupo. O loop externo itera nas chaves de grupo e o loop interno itera em cada item do grupo em si. Um grupo pode ter uma chave sem nenhum elemento. Este é o loop `foreach` que executa a consulta nos exemplos de código anteriores:

[!code-csharp[cscsrefQueryKeywords#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#12)]

## <a name="key-types"></a>Tipos de chave

As chaves de grupo podem ser de qualquer tipo, como uma cadeia de caracteres, um tipo numérico interno, um tipo nomeado definido pelo usuário ou um tipo anônimo.

### <a name="grouping-by-string"></a>Agrupar por cadeia de caracteres

Os exemplos de código anteriores usaram um `char`. Em vez disso, uma chave de cadeia de caracteres pode facilmente ter sido especificada, por exemplo, o sobrenome completo:

[!code-csharp[cscsrefQueryKeywords#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#13)]

### <a name="grouping-by-bool"></a>Agrupar por bool

O exemplo a seguir mostra o uso de um valor booliano para uma chave dividir os resultados em dois grupos. Observe que o valor é produzido por uma subexpressão na cláusula `group`.

[!code-csharp[cscsrefQueryKeywords#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#14)]

### <a name="grouping-by-numeric-range"></a>Agrupar por alcance numérico

O próximo exemplo usa uma expressão para criar chaves de grupo numéricas que representam um intervalo de percentil. Observe o uso de [let](let-clause.md) como um local conveniente para armazenar um resultado de chamada de método, para que não seja necessário chamar o método duas vezes na cláusula `group`. Para obter mais informações sobre como usar métodos em expressões de consulta com segurança, consulte [tratar exceções em expressões de consulta](../../linq/handle-exceptions-in-query-expressions.md).

[!code-csharp[cscsrefQueryKeywords#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#15)]

### <a name="grouping-by-composite-keys"></a>Agrupando por chaves compostas

Use uma chave composta para agrupar elementos de acordo com mais de uma chave. Uma chave composta é criada usando um tipo anônimo ou nomeado para armazenar o elemento-chave. No exemplo a seguir, suponha que uma classe `Person` foi declarada com membros nomeados `surname` e `city`. A cláusula `group` faz com que um grupo separado seja criado para cada conjunto de pessoas com o mesmo sobrenome e a mesma cidade.

```csharp
group person by new {name = person.surname, city = person.city};
```

Use um tipo nomeado se for necessário passar a variável de consulta para outro método. Crie uma classe especial usando as propriedades autoimplementadas das chaves e, em seguida, substitua os métodos <xref:System.Object.Equals%2A> e <xref:System.Object.GetHashCode%2A>. Também é possível usar um struct; nesse caso, não é exatamente necessário substituir esses métodos. Para obter mais informações, consulte [como implementar uma classe leve com propriedades implementadas automaticamente](../../programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md) e [como consultar arquivos duplicados em uma árvore de diretórios](../../programming-guide/concepts/linq/how-to-query-for-duplicate-files-in-a-directory-tree-linq.md). O último artigo apresenta um exemplo de código que demonstra como usar uma chave composta com um tipo nomeado.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra a norma padrão para ordenar dados de origem em grupos quando nenhuma lógica de consulta adicional for aplicada aos grupos. Isso é chamado de “agrupamento sem uma continuação”. Os elementos em uma matriz de cadeias de caracteres são agrupados de acordo com a primeira letra. O resultado da consulta é um tipo <xref:System.Linq.IGrouping%602> que contém uma propriedade `Key` pública do tipo `char` e uma coleção <xref:System.Collections.Generic.IEnumerable%601> que contém cada item no agrupamento.

O resultado de uma cláusula `group` é uma sequência de sequências. Portanto, para acessar os elementos individuais dentro de cada grupo retornado, use um loop aninhado `foreach` dentro do loop que itera as chaves de grupo, conforme mostrado no exemplo a seguir.

[!code-csharp[cscsrefQueryKeywords#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#16)]

## <a name="example"></a>Exemplo

Este exemplo mostra como executar a lógica adicional nos grupos depois criá-los, usando uma *continuação* com `into`. Para obter mais informações, consulte [into](into.md). O exemplo a seguir consulta cada grupo para selecionar apenas aqueles cujo valor da chave é uma vogal.

[!code-csharp[cscsrefQueryKeywords#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Group.cs#17)]

## <a name="remarks"></a>Comentários

No tempo de compilação, as cláusulas `group` são convertidas em chamadas para o método <xref:System.Linq.Enumerable.GroupBy%2A>.

## <a name="see-also"></a>Confira também

- <xref:System.Linq.IGrouping%602>
- <xref:System.Linq.Enumerable.GroupBy%2A>
- <xref:System.Linq.Enumerable.ThenBy%2A>
- <xref:System.Linq.Enumerable.ThenByDescending%2A>
- [Palavras-chave de consulta](query-keywords.md)
- [LINQ (Consulta Integrada à Linguagem)](../../linq/index.md)
- [Criar um grupo aninhado](../../linq/create-a-nested-group.md)
- [Agrupar resultados de consultas](../../linq/group-query-results.md)
- [Executar uma subconsulta em uma operação de agrupamento](../../linq/perform-a-subquery-on-a-grouping-operation.md)
