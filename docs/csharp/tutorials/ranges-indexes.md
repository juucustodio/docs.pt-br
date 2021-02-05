---
title: Explore os intervalos de dados usando intervalos e índices
description: Este tutorial avançado ensina a explorar dados usando índices e intervalos para examinar um intervalo contínuo de um conjunto de dados sequenciais.
ms.date: 09/11/2020
ms.technology: csharp-fundamentals
ms.custom: mvc
ms.openlocfilehash: c0484a42233466e3a2a70a673aee81fce91fe31b
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585397"
---
# <a name="indices-and-ranges"></a>Índices e intervalos

Intervalos e índices fornecem uma sintaxe sucinta para acessar elementos únicos ou intervalos em uma sequência.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
>
> - Use a sintaxe para intervalos em uma sequência.
> - Compreenda as decisões de design para o início e o fim de cada sequência.
> - Conheça cenários para os tipos <xref:System.Index> e <xref:System.Range>.

## <a name="language-support-for-indices-and-ranges"></a>Suporte a idioma para intervalos e índices

Esse suporte a idioma depende de dois novos tipos e de dois novos operadores:

- <xref:System.Index?displayProperty=nameWithType> representa um índice em uma sequência.
- O índice do operador end `^` , que especifica que um índice é relativo ao final de uma sequência.
- <xref:System.Range?displayProperty=nameWithType> representa um subintervalo de uma sequência.
- O operador Range `..` , que especifica o início e o término de um intervalo como seus operandos.

Vamos começar com as regras para índices. Considere uma matriz `sequence`. O índice `0` é o mesmo que `sequence[0]`. O índice `^0` é o mesmo que `sequence[sequence.Length]`. A expressão `sequence[^0]` gera uma exceção, assim como `sequence[sequence.Length]` faz. Para qualquer número `n`, o índice `^n` é o mesmo que `sequence[sequence.Length - n]`.

```csharp
string[] words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

Você pode recuperar a última palavra com o índice `^1`. Adicione o código a seguir abaixo da inicialização:

[!code-csharp[LastIndex](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastIndex)]

Um intervalo especifica o *início* e o *final* de um intervalo. Os intervalos são exclusivos, o que significa que o *final* não está incluído no intervalo. O intervalo `[0..^0]` representa todo o intervalo, assim como `[0..sequence.Length]` representa todo o intervalo.

O código a seguir cria um subintervalo com as palavras "quick", "brown" e "fox". Ele inclui `words[1]` até `words[3]`. O elemento `words[4]` não está no intervalo. Adicione o seguinte código ao mesmo método. Copie e cole-o na parte inferior da janela interativa.

[!code-csharp[Range](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Range)]

O código a seguir retorna o intervalo com "Lazy" e "Dog". Ele inclui `words[^2]` e `words[^1]`. O índice final `words[^0]` não está incluído. Adicione o seguinte código também:

[!code-csharp[LastRange](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastRange)]

Os exemplos a seguir criam intervalos abertos para o início, fim ou ambos:

[!code-csharp[PartialRange](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_PartialRanges)]

Você também pode declarar intervalos ou índices como variáveis. A variável então pode ser usada dentro dos caracteres `[` e `]`:

[!code-csharp[IndexRangeTypes](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_RangeIndexTypes)]

O exemplo a seguir mostra muitos dos motivos para essas escolhas. Modifique `x`, `y` e `z` para tentar combinações diferentes. Quando você testar, use valores em que `x` é menor que `y` e `y` é menor que `z` para as combinações válidas. Adicione o seguinte código a um novo método. Tente usar combinações diferentes:

[!code-csharp[SemanticsExamples](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Semantics)]

## <a name="type-support-for-indices-and-ranges"></a>Suporte de tipo para índices e intervalos

Índices e intervalos fornecem sintaxe clara e concisa para acessar um único elemento ou um intervalo de elementos em uma sequência. Uma expressão de índice normalmente retorna o tipo dos elementos de uma sequência. Uma expressão de intervalo normalmente retorna o mesmo tipo de sequência que a sequência de origem.

Qualquer tipo que fornece um [indexador](../programming-guide/indexers/index.md) com um <xref:System.Index> <xref:System.Range> parâmetro ou dá suporte explicitamente a índices ou intervalos, respectivamente. Um indexador que usa um único <xref:System.Range> parâmetro pode retornar um tipo de sequência diferente, como <xref:System.Span%601?displayProperty=nameWithType> .

> [!IMPORTANT]
> O desempenho do código usando o operador Range depende do tipo do operando de sequência.
>
> A complexidade de tempo do operador de intervalo depende do tipo de sequência. Por exemplo, se a sequência for uma `string` matriz ou, o resultado será uma cópia da seção especificada da entrada, portanto, a complexidade de tempo será *o (n)* (em que N é o comprimento do intervalo). Por outro lado, se for um <xref:System.Span%601?displayProperty=nameWithType> ou um <xref:System.Memory%601?displayProperty=nameWithType> , o resultado faz referência ao mesmo armazenamento de backup, o que significa que não há cópia e a operação é *o (1)*.
>
> Além da complexidade do tempo, isso causa alocações e cópias extras, afetando o desempenho. Em código sensível ao desempenho, considere usar `Span<T>` ou `Memory<T>` como o tipo de sequência, já que o operador de intervalo não é alocado para eles.

Um tipo pode ser **contabilizado** se tiver uma propriedade chamada `Length` ou `Count` com um getter acessível e um tipo de retorno de `int` . Um tipo com contagem que não dá suporte explicitamente a índices ou intervalos pode fornecer um suporte implícito para eles. Para obter mais informações, consulte as seções [suporte ao índice implícito](~/_csharplang/proposals/csharp-8.0/ranges.md#implicit-index-support) e [suporte de intervalo implícito](~/_csharplang/proposals/csharp-8.0/ranges.md#implicit-range-support) da [Nota de proposta de recurso](~/_csharplang/proposals/csharp-8.0/ranges.md). Intervalos usando o suporte de intervalo implícito retornam o mesmo tipo de sequência que a sequência de origem.

Por exemplo, os seguintes tipos .NET oferecem suporte a índices e intervalos: <xref:System.String> , <xref:System.Span%601> e <xref:System.ReadOnlySpan%601> . O <xref:System.Collections.Generic.List%601> dá suporte a índices, mas não dá suporte a intervalos.

<xref:System.Array> tem um comportamento mais nuancedo. Matrizes de dimensão única dão suporte a índices e intervalos. Matrizes multidimensionais não dão suporte a indexadores ou intervalos. O indexador de uma matriz multidimensional tem vários parâmetros, não um único parâmetro. Matrizes denteadas, também chamadas de matriz de matrizes, oferecem suporte a intervalos e indexadores. O exemplo a seguir mostra como iterar uma subseção retangular de uma matriz denteada. Ele itera a seção no centro, excluindo as primeiras e últimas três linhas, e a primeira e a última duas colunas de cada linha selecionada:

[!code-csharp[JaggedArrays](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_JaggedArrays)]

Em todos os casos, o operador Range para <xref:System.Array> aloca uma matriz para armazenar os elementos retornados.

## <a name="scenarios-for-indices-and-ranges"></a>Cenários para índices e intervalos

Você geralmente usará intervalos e índices quando desejar analisar uma parte de uma sequência maior. A nova sintaxe fica mais clara na leitura exata do que parte da seqüência está envolvida. A função local `MovingAverage` usa um <xref:System.Range> como seu argumento. O método então enumera apenas esse intervalo ao calcular o mínimo, máximo e média. Experimente o seguinte código em seu projeto:

[!code-csharp[MovingAverages](~/samples/snippets/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_MovingAverage)]
