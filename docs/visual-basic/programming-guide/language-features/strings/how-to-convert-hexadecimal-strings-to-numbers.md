---
description: 'Saiba mais sobre: como converter cadeias de caracteres hexadecimais em números (Visual Basic)'
title: Como converter cadeias de caracteres hexadecimais em números
ms.date: 01/31/2018
helpviewer_keywords:
- numbers [Visual Basic], hexadecimals
- hexadecimals [Visual Basic], decimals
- examples [Visual Basic], string conversion
- decimals [Visual Basic], hexadecimals
- string conversion [Visual Basic], hexadecimal to numbers
ms.assetid: 76675807-eadb-4c08-bd50-e6c6ff4b8ced
ms.openlocfilehash: cf1648b5f85f189f203f56cf569041e4f2db5ac3
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100425537"
---
# <a name="how-to-convert-hexadecimal-strings-to-numbers-visual-basic"></a>Como converter cadeias de caracteres hexadecimais em números (Visual Basic)

Este exemplo converte uma cadeia de caracteres hexadecimal em um inteiro usando o <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType> método.

## <a name="to-convert-a-hexadecimal-string-to-a-number"></a>Para converter uma cadeia de caracteres hexadecimal em um número

- Use o <xref:System.Convert.ToInt32(System.String,System.Int32)> método para converter o número expresso em base-16 em um inteiro.

  O primeiro argumento do <xref:System.Convert.ToInt32(System.String,System.Int32)> método é a cadeia de caracteres a ser convertida. O segundo argumento descreve em qual base o número é expresso; o hexadecimal é a base 16.

  [!code-vb[VbVbalrStrings#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#62)]

- Observe que a cadeia de caracteres hexadecimal tem as seguintes restrições:

  - Ele não pode incluir o `&h` prefixo.
  - Ele não pode incluir o `_` separador de dígitos.

  Se o prefixo ou um separador de dígitos estiver presente, a chamada para o <xref:System.Convert.ToInt32(System.String,System.Int32)> método lançará um <xref:System.FormatException> .

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.Conversion.Hex%2A>
- <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType>
