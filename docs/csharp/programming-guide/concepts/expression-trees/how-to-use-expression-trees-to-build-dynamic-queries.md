---
title: Consultando com base no estado de tempo de execução (C#)
description: Descreve várias técnicas que seu código pode usar para consultar dinamicamente dependendo do estado de tempo de execução, variando as chamadas de método LINQ ou as árvores de expressão passadas para esses métodos.
ms.date: 02/11/2021
ms.assetid: 52cd44dd-a3ec-441e-b93a-4eca388119c7
ms.openlocfilehash: 0dcf1696ca323ac4823c80c7993fef7873fd8ed5
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100433777"
---
# <a name="querying-based-on-runtime-state-c"></a>Consultando com base no estado de tempo de execução (C#)

Considere o código que define um <xref:System.Linq.IQueryable> ou [um \<T> IQueryable](<xref:System.Linq.IQueryable%601>) em relação a uma fonte de dados:

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Initialize":::

Toda vez que você executar esse código, a mesma consulta exata será executada. Isso geralmente não é muito útil, pois talvez você queira que seu código execute consultas diferentes dependendo das condições em tempo de execução. Este artigo descreve como você pode executar uma consulta diferente com base no estado de tempo de execução.

## <a name="iqueryable--iqueryablet-and-expression-trees"></a>\<T>Árvores de expressão IQueryable/IQueryable

Fundamentalmente, um <xref:System.Linq.IQueryable> tem dois componentes:

* <xref:System.Linq.IQueryable.Expression>&mdash;uma representação independente de linguagem e fonte de fontes dos componentes da consulta atual, na forma de uma árvore de expressão.
* <xref:System.Linq.IQueryable.Provider>&mdash;uma instância de um provedor LINQ, que sabe como materializar a consulta atual em um valor ou conjunto de valores.

No contexto de consulta dinâmica, o provedor geralmente permanecerá o mesmo; a árvore de expressão da consulta será diferente da consulta para consulta.

As árvores de expressão são imutáveis; Se você quiser uma árvore de expressão diferente &mdash; e, portanto, uma consulta diferente &mdash; , precisará traduzir a árvore de expressão existente para uma nova e, portanto, para uma nova <xref:System.Linq.IQueryable> .

As seções a seguir descrevem técnicas específicas para consultar de forma diferente em resposta ao estado de tempo de execução:

- Usar o estado de tempo de execução de dentro da árvore de expressão
- Chamar métodos LINQ adicionais
- Varie a árvore de expressão passada para os métodos LINQ
- Construa uma árvore de expressão de [expressão \<TDelegate> ](xref:System.Linq.Expressions.Expression%601) usando os métodos de fábrica em<xref:System.Linq.Expressions.Expression>
- Adicionando nós de chamada de método à <xref:System.Linq.IQueryable> árvore de expressão de uma
- Construir cadeias de caracteres e usar a [biblioteca dinâmica do LINQ](https://dynamic-linq.net/)

## <a name="use-runtime-state-from-within-the-expression-tree"></a>Usar o estado de tempo de execução de dentro da árvore de expressão

Supondo que o provedor LINQ ofereça suporte a ele, a maneira mais simples de consultar dinamicamente é referenciar o estado de tempo de execução diretamente na consulta por meio de uma variável fechada, como `length` no exemplo de código a seguir:

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Runtime_state_from_within_expression_tree":::

A árvore de expressão interna &mdash; e, portanto, a consulta &mdash; não foi modificada; a consulta retorna valores diferentes somente porque o valor de `length` foi alterado.

## <a name="call-additional-linq-methods"></a>Chamar métodos LINQ adicionais

Em geral, os [métodos internos do LINQ](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Linq.Queryable/src/System/Linq/Queryable.cs) em <xref:System.Linq.Queryable> executam duas etapas:

* Encapsula a árvore de expressão atual em uma <xref:System.Linq.Expressions.MethodCallExpression> representando a chamada de método.
* Passe a árvore de expressão encapsulada de volta para o provedor, para retornar um valor por meio do método do provedor <xref:System.Linq.IQueryProvider.Execute%2A?displayProperty=nameWithType> ; ou para retornar um objeto de consulta traduzido por meio do <xref:System.Linq.IQueryProvider.CreateQuery%2A?displayProperty=nameWithType> método.

Você pode substituir a consulta original pelo resultado de um método de retorno [IQueryable \<T> ](xref:System.Linq.IQueryable%601)para obter uma nova consulta. Você pode fazer isso com base no estado de tempo de execução, como no exemplo a seguir:

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Added_method_calls":::

## <a name="vary-the-expression-tree-passed-into-the-linq-methods"></a>Varie a árvore de expressão passada para os métodos LINQ

Você pode passar expressões diferentes para os métodos LINQ, dependendo do estado de tempo de execução:

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Varying_expressions":::

Talvez você também queira compor as várias subexpressãos usando uma biblioteca de terceiros, como o [PredicateBuilder](http://www.albahari.com/nutshell/predicatebuilder.aspx)da [LinqKit](http://www.albahari.com/nutshell/linqkit.aspx):

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Compose_expressions":::

## <a name="construct-expression-trees-and-queries-using-factory-methods"></a>Construir árvores e consultas de expressão usando métodos de fábrica

Em todos os exemplos até esse ponto, nós conhecidas o tipo de elemento no momento da compilação &mdash; `string` &mdash; e, portanto, o tipo da consulta &mdash; `IQueryable<string>` . Talvez seja necessário adicionar componentes a uma consulta de qualquer tipo de elemento. Talvez seja necessário adicionar componentes diferentes, dependendo do tipo de elemento. Você pode criar árvores de expressão do zero, usando os métodos de fábrica em <xref:System.Linq.Expressions.Expression?displayProperty=fullName> e, portanto, personalizar a expressão para um tipo de elemento específico.

### <a name="constructing-an-expressiontdelegate"></a>Construindo uma [expressão \<TDelegate> ](xref:System.Linq.Expressions.Expression%601)

Quando você constrói uma expressão para passar em um dos métodos LINQ, na verdade está construindo uma instância de [Expression \<TDelegate> ](xref:System.Linq.Expressions.Expression%601), em que `TDelegate` é um tipo delegado, como `Func<string, bool>` , `Action` ou um tipo de delegado personalizado.

[Expressão \<TDelegate> ](xref:System.Linq.Expressions.Expression%601) de herda de <xref:System.Linq.Expressions.LambdaExpression> , que representa uma expressão lambda completa como a seguinte:

```csharp
Expression<Func<string, bool>> expr = x => x.StartsWith("a");
```

Um <xref:System.Linq.Expressions.LambdaExpression> tem dois componentes:

* uma lista de parâmetros &mdash; `(string x)` &mdash; representada pela <xref:System.Linq.Expressions.LambdaExpression.Parameters> Propriedade
* um corpo &mdash; `x.StartsWith("a")` &mdash; representado pela <xref:System.Linq.Expressions.LambdaExpression.Body> propriedade.

As etapas básicas na construção de uma [expressão \<TDelegate> ](xref:System.Linq.Expressions.Expression%601) são as seguintes:

* Defina <xref:System.Linq.Expressions.ParameterExpression> objetos para cada um dos parâmetros (se houver) na expressão lambda, usando o <xref:System.Linq.Expressions.Expression.Parameter%2A> método de fábrica.

    ```csharp
    ParameterExpression x = Parameter(typeof(string), "x");
    ```

* Construa o corpo do seu <xref:System.Linq.Expressions.LambdaExpression> , usando o <xref:System.Linq.Expressions.ParameterExpression> que você definiu. Por exemplo, uma expressão que representa `x.StartsWith("a")` poderia ser construída da seguinte maneira:

    ```csharp
    Expression body = Call(
        x,
        typeof(string).GetMethod("StartsWith", new [] {typeof(string)}),
        Constant("a")
    );
    ```

* Empacote os parâmetros e o corpo em uma [expressão \<TDelegate> ](xref:System.Linq.Expressions.Expression%601)de tipo de tempo de compilação, usando a <xref:System.Linq.Expressions.Expression.Lambda%2A> sobrecarga de método de fábrica apropriada:

    ```csharp
    Expression<Func<string, bool>> expr = Lambda<Func<string, bool>>(body, prm);
    ```

As seções a seguir descrevem um cenário no qual você pode querer construir uma [expressão \<TDelegate> ](xref:System.Linq.Expressions.Expression%601) para passar para um método LINQ e fornecer um exemplo completo de como fazer isso usando os métodos de fábrica.

### <a name="scenario"></a>Cenário

Digamos que você tenha vários tipos de entidade:

```csharp
record Person(string LastName, string FirstName, DateTime DateOfBirth);
record Car(string Model, int Year);
```

Para qualquer um desses tipos de entidade, você deseja filtrar e retornar somente as entidades que têm um determinado texto dentro de um de seus `string` campos. Para `Person` o, você desejaria Pesquisar `FirstName` as `LastName` Propriedades e:

```csharp
string term = /* ... */;
var personsQry = new List<Person>()
    .AsQueryable()
    .Where(x => x.FirstName.Contains(term) || x.LastName.Contains(term));
```

Mas `Car` , para o, você desejaria Pesquisar apenas a `Model` Propriedade:

```csharp
string term = /* ... */;
var carsQry = new List<Car>()
    .AsQueryable()
    .Where(x => x.Model.Contains(term));
```

Embora você possa escrever uma função personalizada para `IQueryable<Person>` o e outra para `IQueryable<Car>` o, a função a seguir adiciona essa filtragem a qualquer consulta existente, independentemente do tipo de elemento específico.

### <a name="example"></a>Exemplo

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Factory_methods_expression_of_tdelegate":::

Como a `TextFilter` função usa e retorna um [IQueryable \<T> ](xref:System.Linq.IQueryable%601) (e não apenas um <xref:System.Linq.IQueryable> ), você pode adicionar elementos de consulta de tipo de tempo de compilação adicionais após o filtro de texto.

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Factory_methods_expression_of_tdelegate_usage":::

## <a name="adding-method-call-nodes-to-the-xrefsystemlinqiqueryables-expression-tree"></a>Adicionando nós de chamada de método à <xref:System.Linq.IQueryable> árvore de expressão do

Se você tiver um <xref:System.Linq.IQueryable> em vez de [um \<T> IQueryable](xref:System.Linq.IQueryable%601), não poderá chamar diretamente os métodos LINQ genéricos. Uma alternativa é criar a árvore de expressão interna como acima e usar a reflexão para invocar o método LINQ apropriado ao passar na árvore de expressão.

Você também pode duplicar a funcionalidade do método LINQ, encapsulando a árvore inteira em um <xref:System.Linq.Expressions.MethodCallExpression> que representa uma chamada para o método LINQ:

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Factory_methods_lambdaexpression":::

Observe que, nesse caso, você não tem um espaço reservado genérico de tempo de compilação `T` , portanto, você usará a <xref:System.Linq.Expressions.Expression.Lambda%2A> sobrecarga que não requer informações de tipo de tempo de compilação e que produz um <xref:System.Linq.Expressions.LambdaExpression> em vez de uma [expressão \<TDelegate> ](xref:System.Linq.Expressions.Expression%601).

## <a name="the-dynamic-linq-library"></a>A biblioteca do LINQ dinâmico

A construção de árvores de expressão usando métodos de fábrica é relativamente complexa; é mais fácil compor cadeias de caracteres. A [biblioteca LINQ dinâmica](https://dynamic-linq.net/) expõe um conjunto de métodos de extensão no <xref:System.Linq.IQueryable> correspondente aos métodos padrão do LINQ em <xref:System.Linq.Queryable> e que aceitam cadeias de caracteres em uma [sintaxe especial](https://dynamic-linq.net/expression-language) em vez de árvores de expressão. A biblioteca gera a árvore de expressão apropriada a partir da cadeia de caracteres e pode retornar a tradução resultante <xref:System.Linq.IQueryable> .

Por exemplo, o exemplo anterior poderia ser reescrito da seguinte maneira:

:::code language="csharp" source="../../../../../samples/snippets/csharp/programming-guide/dynamic-linq-expression-trees/Program.cs" id="Dynamic_linq":::

## <a name="see-also"></a>Consulte também

- [Árvores de expressão (C#)](./index.md)
- [Como executar árvores de expressão (C#)](./how-to-execute-expression-trees.md)
- [Especificar filtros predicados dinamicamente em runtime](../../../linq/dynamically-specify-predicate-filters-at-runtime.md)
