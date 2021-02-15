---
title: Genéricos e matrizes – Guia de Programação em C#
description: Saiba mais sobre genéricos e matrizes na programação em C#. Confira exemplos de código e exiba recursos adicionais disponíveis.
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], arrays
- arrays [C#], generics
ms.assetid: 7d956536-3851-41b5-94ad-3e7c0a5fe485
ms.openlocfilehash: 808e9ddafea9806a74ccd105c8850e7b77b563be
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91151448"
---
# <a name="generics-and-arrays-c-programming-guide"></a>Genéricos e matrizes (Guia de Programação em C#)

No C# 2.0 e versões posteriores, matrizes unidimensionais que têm um limite inferior a zero implementam <xref:System.Collections.Generic.IList%601> automaticamente. Isso permite a criação de métodos genéricos que podem usar o mesmo código para iterar por meio de matrizes e outros tipos de coleção. Essa técnica é útil principalmente para ler dados em coleções. A interface <xref:System.Collections.Generic.IList%601> não pode ser usada para adicionar ou remover elementos de uma matriz. Uma exceção será lançada se você tentar chamar um método <xref:System.Collections.Generic.IList%601> tal como <xref:System.Collections.Generic.IList%601.RemoveAt%2A> em uma matriz neste contexto.  
  
 O exemplo de código a seguir demonstra como um único método genérico que usa um parâmetro de entrada <xref:System.Collections.Generic.IList%601> pode iterar por meio de uma lista e uma matriz, nesse caso, uma matriz de inteiros.  
  
 [!code-csharp[csProgGuideGenerics#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#35)]  
  
## <a name="see-also"></a>Confira também

- <xref:System.Collections.Generic>
- [Guia de programação C#](../index.md)
- [Genéricos](./index.md)
- [matrizes](../arrays/index.md)
- [Genéricos](../../../standard/generics/index.md)
