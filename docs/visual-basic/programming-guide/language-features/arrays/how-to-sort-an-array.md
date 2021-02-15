---
description: 'Saiba mais sobre: como classificar uma matriz no Visual Basic'
title: Como classificar matrizes
ms.date: 07/20/2015
f1_keywords:
- Array.Sort
helpviewer_keywords:
- arrays [Visual Basic], sorting
- examples [Visual Basic], arrays
ms.assetid: 9289aeaa-9626-4698-94a7-1d1fd3702b87
ms.openlocfilehash: ea030b63dbbb5f5ea1d6160757afe2e9b58f7c21
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100462757"
---
# <a name="how-to-sort-an-array-in-visual-basic"></a>Como classificar uma matriz no Visual Basic

Este artigo mostra um exemplo de como classificar uma matriz de cadeias de caracteres no Visual Basic.

## <a name="example"></a>Exemplo

Este exemplo declara uma matriz de `String` objetos chamada `zooAnimals` , popula-o e, em seguida, classifica-o em ordem alfabética:
  
```vb
Private Sub SortAnimals()
    Dim zooAnimals(2) As String
    zooAnimals(0) = "lion"
    zooAnimals(1) = "turtle"
    zooAnimals(2) = "ostrich"
    Array.Sort(zooAnimals)
End Sub
```

## <a name="robust-programming"></a>Programação robusta

As seguintes condições podem causar uma exceção:

- A matriz está vazia ( <xref:System.ArgumentNullException> classe).
- A matriz é multidimensional ( <xref:System.RankException> classe).
- Um ou mais elementos da matriz não implementam a <xref:System.IComparable> interface ( <xref:System.InvalidOperationException> classe).

## <a name="see-also"></a>Consulte também

- <xref:System.Array.Sort%2A?displayProperty=nameWithType>
- [matrizes](index.md)
- [Solução de problemas de matrizes](troubleshooting-arrays.md)
- [Coleções](../../concepts/collections.md)
- [Instrução For Each...Next](../../../language-reference/statements/for-each-next-statement.md)
