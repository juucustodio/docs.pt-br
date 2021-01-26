---
title: Matrizes – Guia de Programação em C#
description: Armazene várias variáveis do mesmo tipo em uma estrutura de dados de matriz em C#. Declare uma matriz especificando um tipo ou especifique um objeto para armazenar qualquer tipo.
ms.date: 01/22/2021
helpviewer_keywords:
- arrays [C#]
- C# language, arrays
ms.assetid: bb79bdde-e570-4c30-adb0-1dd5759ae041
ms.openlocfilehash: 203d8b86da4e74d8c5397132a0ba68618eedf348
ms.sourcegitcommit: 4d5e25a46aa7cd0d29b4b9227b92987354d444c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98794763"
---
# <a name="arrays-c-programming-guide"></a>Matrizes (Guia de Programação em C#)

Você pode armazenar diversas variáveis do mesmo tipo em uma estrutura de dados de matriz. Você pode declarar uma matriz especificando o tipo de seus elementos. Se você quiser que a matriz armazene elementos de qualquer tipo, você pode especificar `object` como seu tipo. No sistema de tipos unificado do C#, todos os tipos, predefinidos e definidos pelo usuário, tipos de referência e tipos de valor, herdam direta ou indiretamente de <xref:System.Object>.

```csharp
type[] arrayName;
```

## <a name="example"></a>Exemplo

O exemplo a seguir cria matrizes unidimensionais, multidimensionais e denteadas:

[!code-csharp[csProgGuideArrays#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#1)]

## <a name="array-overview"></a>Visão geral da matriz

Uma matriz tem as seguintes propriedades:

- Uma matriz pode ser [única](single-dimensional-arrays.md), [multidimensional](multidimensional-arrays.md) ou [denteada](jagged-arrays.md).
- O número de dimensões e o tamanho de cada dimensão são estabelecidos quando a instância de matriz é criada. Esses valores não podem ser alterados durante o ciclo de vida da instância.
- Os valores padrão dos elementos de matriz numérica são definidos como zero, e os elementos de referência são definidos como null.
- Uma matriz denteada é uma matriz de matrizes e, portanto, seus elementos são tipos de referência e são inicializados para `null`.
- As matrizes são indexadas por zero: uma matriz com elementos `n` é indexada de `0` para `n-1`.
- Os elementos de matriz podem ser de qualquer tipo, inclusive um tipo de matriz.
- Os tipos de matriz são [tipos de referência](../../language-reference/keywords/reference-types.md) derivados do tipo base abstrato <xref:System.Array>. Como esse tipo implementa <xref:System.Collections.IEnumerable> e <xref:System.Collections.Generic.IEnumerable%601>, você pode usar a iteração [foreach](../../language-reference/keywords/foreach-in.md) em todas as matrizes em c#.

### <a name="arrays-as-objects"></a>Matrizes como Objetos

No C#, as matrizes são objetos e não apenas regiões endereçáveis de memória contígua, como no C e no C++. <xref:System.Array> é o tipo base abstrato de todos os tipos de matriz. Você pode usar as propriedades e outros membros da classe que o <xref:System.Array> tem. Um exemplo disso é usar a <xref:System.Array.Length%2A> propriedade para obter o comprimento de uma matriz. O código a seguir atribui o comprimento da matriz `numbers`, que é `5`, a uma variável denominada `lengthOfNumbers`:

[!code-csharp[csProgGuideArrays#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#3)]

A classe <xref:System.Array> fornece vários outros métodos e propriedades úteis para classificar, pesquisar e copiar matrizes. O exemplo a seguir usa a <xref:System.Array.Rank%2A> propriedade para exibir o número de dimensões de uma matriz.

[!code-csharp[csProgGuideArrays#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#2)]

## <a name="see-also"></a>Confira também

- [Como usar matrizes unidimensionais](single-dimensional-arrays.md)
- [Como usar matrizes multidimensionais](multidimensional-arrays.md)
- [Como usar matrizes denteadas](jagged-arrays.md)
- [Usando foreach com matrizes](using-foreach-with-arrays.md)
- [Passando matrizes como argumentos](passing-arrays-as-arguments.md)
- [Matrizes digitadas implicitamente](implicitly-typed-arrays.md)
- [Guia de programação C#](../index.md)
- [Coleções](../concepts/collections.md)

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]
