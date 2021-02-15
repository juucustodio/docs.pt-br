---
title: LINQ (consulta integrada à linguagem) em C#
description: Apresenta a LINQ (consulta integrada à linguagem) em C#.
ms.date: 11/30/2016
ms.assetid: 007cc736-f5cf-4919-b99b-0c00ab2814ce
ms.openlocfilehash: b39aeffa4871d523679162497a7a4e81cf1293ca
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90545950"
---
# <a name="language-integrated-query-linq"></a>LINQ (Consulta Integrada à Linguagem)

O LINQ (consulta integrada à linguagem) é o nome de um conjunto de tecnologias com base na integração de recursos de consulta diretamente na linguagem C#. Tradicionalmente, consultas feitas em dados são expressas como cadeias de caracteres simples sem verificação de tipo no tempo de compilação ou suporte a IntelliSense. Além disso, você precisará aprender uma linguagem de consulta diferente para cada tipo de fonte de dados: bancos de dados SQL, documentos XML, vários serviços Web etc. Com o LINQ, uma consulta é um constructo de linguagem de primeira classe, como classes, métodos, eventos.

Para um desenvolvedor que escreve consultas, a parte mais visível "integrada à linguagem" do LINQ é a expressão de consulta. As expressões de consulta são uma *sintaxe declarativa de consulta*. Usando a sintaxe de consulta, você pode executar operações de filtragem, ordenação e agrupamento em fontes de dados com o mínimo de código. Você pode usar os mesmos padrões de expressão de consulta básica para consultar e transformar dados em bancos de dados SQL, conjuntos de dados do ADO.NET, documentos XML e fluxos e coleções .NET.

O exemplo a seguir mostra a operação de consulta completa. A operação completa inclui a criação de uma fonte de dados, definição da expressão de consulta e execução da consulta em uma instrução `foreach`.

[!code-csharp[csProgGuideLINQ#11](~/samples/snippets/csharp/concepts/linq/index_1.cs)]

## <a name="query-expression-overview"></a>Visão geral da expressão de consulta

- Expressões de consulta podem ser usadas para consultar e transformar dados de qualquer fonte de dados habilitada para LINQ. Por exemplo, uma única consulta pode recuperar dados de um Banco de Dados SQL e produzir um fluxo XML como saída.

- As expressões de consulta são fáceis de entender porque elas usam muitos constructos de linguagem C# familiares.

- As variáveis em uma expressão de consulta são fortemente tipadas, embora em muitos casos você não precise fornecer o tipo explicitamente, pois o compilador pode inferir nele. Para obter mais informações, consulte [relações de tipo em operações de consulta LINQ](../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).

- Uma consulta não é executada até que você itere sobre a variável de consulta, por exemplo, em uma instrução `foreach`. Para obter mais informações, consulte [introdução às consultas LINQ](../programming-guide/concepts/linq/introduction-to-linq-queries.md).

- No tempo de compilação, as expressões de consulta são convertidas em chamadas de método do operador de consulta padrão de acordo com as regras definidas na especificação do C#. Qualquer consulta que pode ser expressa usando sintaxe de consulta também pode ser expressa usando sintaxe de método. No entanto, na maioria dos casos, a sintaxe de consulta é mais legível e concisa. Para obter mais informações, consulte [Especificação da linguagem C#](~/_csharplang/spec/expressions.md#query-expressions) e [Visão geral de operadores de consulta padrão](../programming-guide/concepts/linq/standard-query-operators-overview.md).

- Como uma regra ao escrever consultas LINQ, recomendamos que você use a sintaxe de consulta sempre que possível e a sintaxe de método sempre que necessário. Não há semântica ou diferença de desempenho entre as duas formas. As expressões de consulta são geralmente mais legíveis do que as expressões equivalentes escritas na sintaxe de método.

- Algumas operações de consulta, como <xref:System.Linq.Enumerable.Count%2A> ou <xref:System.Linq.Enumerable.Max%2A>, não apresentam cláusulas de expressão de consulta equivalentes e, portanto, devem ser expressas como chamadas de método. A sintaxe de método pode ser combinada com a sintaxe de consulta de várias maneiras. Para obter mais informações, consulte [sintaxe de consulta e sintaxe de método em LINQ](../programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md).

- As expressões de consulta podem ser compiladas para árvores de expressão ou delegados, dependendo do tipo ao qual a consulta é aplicada. As consultas <xref:System.Collections.Generic.IEnumerable%601> são compiladas para representantes. As consultas <xref:System.Linq.IQueryable> e <xref:System.Linq.IQueryable%601> são compiladas para árvores de expressão. Para obter mais informações, consulte [Árvores de expressão](../expression-trees.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais detalhes sobre o LINQ, comece se familiarizando com alguns conceitos básicos em [Noções básicas sobre expressões de consulta](query-expression-basics.md), e, em seguida, leia a documentação para a tecnologia LINQ na qual você está interessado:

- Documentos XML: [LINQ to XML](../../standard/linq/linq-xml-overview.md)

- ADO.NET Entity Framework: [LINQ to Entities](../../framework/data/adonet/ef/language-reference/linq-to-entities.md)

- Coleções do .NET, arquivos, cadeias de caracteres, etc.: [LINQ to Objects](../programming-guide/concepts/linq/linq-to-objects.md)

Para saber mais sobre o LINQ, consulte [LINQ em C#](linq-in-csharp.md).

Para começar a trabalhar com o LINQ em C#, consulte o tutorial [Trabalhando com LINQ](../tutorials/working-with-linq.md).
