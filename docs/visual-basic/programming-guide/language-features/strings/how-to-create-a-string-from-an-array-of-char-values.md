---
description: 'Saiba mais sobre: como criar uma cadeia de caracteres de uma matriz de valores char (Visual Basic)'
title: Como criar uma cadeia de caracteres a partir de uma matriz de valores de caracteres
ms.date: 07/20/2015
helpviewer_keywords:
- examples [Visual Basic], arrays
- examples [Visual Basic], Char data type
ms.assetid: 69f94e85-d57c-4ccc-a62a-426e829f5c5e
ms.openlocfilehash: 67b675f5f02c92b785e374b99f49248d43d12fb4
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100429826"
---
# <a name="how-to-create-a-string-from-an-array-of-char-values-visual-basic"></a>Como criar uma cadeia de caracteres a partir de uma matriz de valores de caracteres (Visual Basic)

Este exemplo cria a cadeia "abcd" de caracteres individuais.  
  
## <a name="example"></a>Exemplo  

 [!code-vb[VbVbalrStrings#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#61)]  
  
## <a name="compile-the-code"></a>Compilar o código  

 Esse método não tem requisitos especiais.  
  
 A sintaxe `"a"c` , em que um único `c` segue um único caractere entre aspas, é usada para criar um literal de caractere.  
  
## <a name="robust-programming"></a>Programação robusta  

 Caracteres nulos (equivalente a `Chr(0)` ) na cadeia de caracteres levam a resultados inesperados ao usar a cadeia de caracteres. O caractere nulo será incluído com a cadeia de caracteres, mas os caracteres após o caractere nulo não serão exibidos em algumas situações.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.String>
- [Tipo de Dados de Caractere](../../../language-reference/data-types/char-data-type.md)
- [Data Types](../data-types/index.md)
