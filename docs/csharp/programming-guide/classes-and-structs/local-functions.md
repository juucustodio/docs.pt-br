---
title: Funções locais – Guia de Programação em C#
description: As funções locais em C# são métodos privados que são aninhados em outro membro e podem ser chamados de seus membros que os contêm.
ms.date: 10/16/2020
helpviewer_keywords:
- local functions [C#]
ms.openlocfilehash: 75accda2e40443073274ece4d8964c13a0945dad
ms.sourcegitcommit: dfcbc096ad7908cd58a5f0aeabd2256f05266bac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92332894"
---
# <a name="local-functions-c-programming-guide"></a>Funções locais (Guia de Programação em C#)

Começando com o C# 7.0, o C# é compatível com *funções locais*. Funções locais são métodos privados de um tipo que estão aninhados em outro membro. Eles só podem ser chamados do membro que os contém. Funções locais podem ser declaradas em e chamadas de:

- Métodos, especialmente os métodos iteradores e os métodos assíncronos
- Construtores
- Acessadores de propriedades
- Acessadores de eventos
- Métodos anônimos
- Expressões lambda
- Finalizadores
- Outras funções locais

No entanto, as funções locais não podem ser declaradas dentro de um membro apto para expressão.

> [!NOTE]
> Em alguns casos, você pode usar uma expressão lambda para implementar uma funcionalidade que também tem suporte por uma função local. Para obter uma comparação, consulte [funções locais versus expressões lambda](#local-functions-vs-lambda-expressions).

Funções locais tornam a intenção do seu código clara. Qualquer pessoa que ler seu código poderá ver que o método não pode ser chamado, exceto pelo método que o contém. Para projetos de equipe, elas também impossibilitam que outro desenvolvedor chame o método por engano diretamente de qualquer outro lugar na classe ou no struct.

## <a name="local-function-syntax"></a>Sintaxe de função local

Uma função local é definida como um método aninhado dentro de um membro recipiente. Sua definição tem a seguinte sintaxe:

```csharp
<modifiers> <return-type> <method-name> <parameter-list>
```

Você pode usar os seguintes modificadores com uma função local:

- [`async`](../../language-reference/keywords/async.md)
- [`unsafe`](../../language-reference/keywords/unsafe.md)
- [`static`](../../language-reference/keywords/static.md) (em C# 8,0 e posterior). Uma função local estática não pode capturar variáveis locais ou estado de instância.
- [`extern`](../../language-reference/keywords/extern.md) (em C# 9,0 e posterior). Uma função local externa deve ser `static` .

Todas as variáveis locais que são definidas no membro recipiente, incluindo seus parâmetros de método, são acessíveis em uma função local não estática.

Ao contrário de uma definição de método, uma definição de função local não pode incluir o modificador de acesso de membro. Já que todas as funções locais são privadas, incluir um modificador de acesso como a palavra-chave `private` gera o erro do compilador CS0106, "O modificador 'private' não é válido para este item".

O exemplo a seguir define uma função local chamada `AppendPathSeparator` que é privada para um método chamado `GetText`:

:::code language="csharp" source="snippets/local-functions/Program.cs" id="Basic" :::

A partir do C# 9,0, você pode aplicar atributos a uma função local, seus parâmetros e parâmetros de tipo, como mostra o exemplo a seguir:

:::code language="csharp" source="snippets/local-functions/Program.cs" id="WithAttributes" :::

O exemplo anterior usa um [atributo especial](../../language-reference/attributes/nullable-analysis.md) para auxiliar o compilador em análise estática em um contexto anulável.

## <a name="local-functions-and-exceptions"></a>Funções locais e exceções

Um dos recursos úteis de funções locais é que elas podem permitir que exceções sejam apresentadas imediatamente. Para iteradores de método, as exceções são apresentadas somente quando a sequência retornada é enumerada e não quando o iterador é recuperado. Para métodos assíncronos, as exceções geradas em um método assíncrono são observadas quando a tarefa retornada é esperada.

O exemplo a seguir define um `OddSequence` método que enumera números ímpares em um intervalo especificado. Já que ele passa um número maior que 100 para o método enumerador `OddSequence`, o método gera uma <xref:System.ArgumentOutOfRangeException>. Assim como demonstrado pela saída do exemplo, a exceção é apresentada somente quando você itera os números e não quando você recupera o enumerador.

:::code language="csharp" source="snippets/local-functions/IteratorWithoutLocal.cs" :::

Se você colocar a lógica do iterador em uma função local, as exceções de validação de argumento serão geradas quando você recuperar o enumerador, como mostra o exemplo a seguir:

:::code language="csharp" source="snippets/local-functions/IteratorWithLocal.cs" :::

Você pode usar funções locais de maneira semelhante com operações assíncronas. Exceções geradas em uma superfície de método assíncrono quando a tarefa correspondente é esperada. Funções locais permitem que seu código falhe no modo rápido e permitem que a exceção seja gerada e observada de forma síncrona.

O exemplo a seguir usa um método assíncrono chamado `GetMultipleAsync` para pausar para um número especificado de segundos e retornar um valor que é um múltiplo aleatório desse número de segundos. O atraso máximo é de 5 segundos; um <xref:System.ArgumentOutOfRangeException> resulta em se o valor for maior que 5. Como mostra o exemplo a seguir, a exceção gerada quando um valor de 6 é passado para o `GetMultipleAsync` método é observada somente quando a tarefa é esperada.

:::code language="csharp" source="snippets/local-functions/AsyncWithoutLocal.cs" :::

Assim como com o iterador de método, você pode refatorar o exemplo anterior e colocar o código da operação assíncrona em uma função local. Como a saída do exemplo a seguir mostra, o <xref:System.ArgumentOutOfRangeException> é lançado assim que o `GetMultiple` método é chamado.

:::code language="csharp" source="snippets/local-functions/AsyncWithLocal.cs" :::

## <a name="local-functions-vs-lambda-expressions"></a>Funções locais vs. expressões lambda

À primeira vista, funções locais e [expressões lambda](../../language-reference/operators/lambda-expressions.md) são muito semelhantes. Em muitos casos, a escolha entre usar expressões lambda e funções locais é uma questão de estilo e preferência pessoal. No entanto, há diferenças reais nos casos em que você pode usar uma ou outra, e é importante conhecer essas diferenças.

Examinaremos as diferenças entre a função local e as implementações de expressão lambda do algoritmo fatorial. Veja a versão usando uma função local:

:::code language="csharp" source="snippets/local-functions/Program.cs" id="FactorialWithLocal" :::

Esta versão usa expressões lambda:

:::code language="csharp" source="snippets/local-functions/Program.cs" id="FactorialWithLambda" :::

### <a name="naming"></a>Nomenclatura

As funções locais são explicitamente nomeadas como métodos. As expressões lambda são métodos anônimos e precisam ser atribuídas a variáveis de um `delegate` tipo, normalmente `Action` ou `Func` tipos. Quando você declara uma função local, o processo é como escrever um método normal; Você declara um tipo de retorno e uma assinatura de função.

### <a name="function-signatures-and-lambda-expression-types"></a>Assinaturas de função e tipos de expressão lambda

Expressões lambda dependem do tipo da `Action` / `Func` variável que são atribuídas para determinar o argumento e os tipos de retorno. Em funções locais, como a sintaxe é muito parecida com a escrita de um método normal, tipos de argumento e tipo de retorno já fazem parte da declaração da função.

### <a name="definite-assignment"></a>Atribuição definida

Expressões lambda são objetos declarados e atribuídos em tempo de execução. Para que uma expressão lambda seja usada, ela precisa ser definitivamente atribuída: a `Action` / `Func` variável à qual ela será atribuída deve ser declarada e a expressão lambda atribuída a ela. Observe que `LambdaFactorial` o deve declarar e inicializar a expressão lambda `nthFactorial` antes de defini-la. Não fazer isso resulta em um erro em tempo de compilação para referenciar `nthFactorial` antes de atribuí-lo.

As funções locais são definidas no momento da compilação. Como eles não são atribuídos a variáveis, eles podem ser referenciados de qualquer local de código **em que esteja no escopo**; em nosso primeiro exemplo `LocalFunctionFactorial` , poderíamos declarar nossa função local acima ou abaixo da `return` instrução e não disparar nenhum erro de compilador.

Essas diferenças significam que os algoritmos recursivos são mais fáceis de criar usando funções locais. Você pode declarar e definir uma função local que chame a si mesma. As expressões lambda devem ser declaradas e atribuídas a um valor padrão antes que possam ser reatribuídas a um corpo que referencie a mesma expressão lambda.

### <a name="implementation-as-a-delegate"></a>Implementação como um delegado

As expressões lambda são convertidas em delegados quando são declaradas. As funções locais são mais flexíveis, pois podem ser escritas como um método tradicional *ou* como um delegado. As funções locais só são convertidas em delegados quando ***usadas*** como um delegado.

Se você declarar uma função local e só referenciá-la ao chamá-la como um método, ela não será convertida em um delegado.

### <a name="variable-capture"></a>Captura de variável

As regras de [atribuição definitiva](../../../../_csharplang/spec/variables.md#definite-assignment) também afetam qualquer variável capturada pela função local ou expressão lambda. O compilador pode executar uma análise estática que permite que as funções locais atribuam definitivamente variáveis capturadas no escopo delimitador. Considere este exemplo:

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

O compilador pode determinar que `LocalFunction` definitivamente atribua `y` quando chamada. Como a `LocalFunction` é chamada antes da instrução `return`, `y` é atribuído definitivamente na instrução `return`.

Observe que quando uma função local captura variáveis no escopo delimitador, a função local é implementada como um tipo delegado.

### <a name="heap-allocations"></a>Alocações de heap

Dependendo do uso, as funções locais podem evitar as alocações de heap que são sempre necessárias nas expressões lambda. Se uma função local nunca for convertida em um delegado, e nenhuma das variáveis capturadas pela função local forem capturadas por outras lambdas ou funções locais que são convertidas em delegados, o compilador poderá evitar alocações de heap.

Considere este exemplo assíncrono:

:::code language="csharp" source="snippets/local-functions/Program.cs" id="AsyncWithLambda" :::

O fechamento desta expressão lambda contém as variáveis `address`, `index` e `name`. No caso de funções locais, o objeto que implementa o encerramento pode ser um tipo `struct`. Esse tipo de struct seria passado por referência à função local. Essa diferença na implementação poderia economizar em uma alocação.

A instanciação necessária para expressões lambda ocasiona alocações adicionais de memória, tornando-se um fator de desempenho em caminhos de código com tempo crítico. As funções locais não incorrem nessa sobrecarga. No exemplo acima, a versão das funções locais tem duas alocações menores do que a versão da expressão lambda.

Se você souber que a função local não será convertida em um delegado e nenhuma das variáveis capturadas por ela for capturada por outras lambdas ou funções locais que são convertidas em delegados, você poderá garantir que a função local Evite ser alocada no heap declarando-a como uma `static` função local. Observe que esse recurso está disponível em C# 8,0 e mais recente.

> [!NOTE]
> A função local equivalente desse método também usa uma classe para o fechamento. O fechamento de uma função local ser implementado como um `class` ou como um `struct`, trata-se de um detalhe de implementação. Uma função local pode usar um `struct`, enquanto uma lambda sempre usará um `class`.

:::code language="csharp" source="snippets/local-functions/Program.cs" id="AsyncWithLocal" :::

### <a name="usage-of-the-yield-keyword"></a>Uso da `yield` palavra-chave

Uma vantagem final não demonstrada neste exemplo é que as funções locais podem ser implementadas como iteradores, usando a sintaxe `yield return` para produzir uma sequência de valores.

:::code language="csharp" source="snippets/local-functions/Program.cs" id="YieldReturn" :::

A `yield return` instrução não é permitida em expressões lambda, consulte o [erro do compilador CS1621](../../misc/cs1621.md).

Embora as funções locais possam parecer redundantes para expressões lambda, elas realmente têm finalidades e usos diferentes. As funções locais são mais eficientes para quando você deseja escrever uma função que é chamada apenas do contexto de outro método.

## <a name="see-also"></a>Consulte também

- [Métodos](methods.md)
