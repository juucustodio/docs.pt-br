---
description: 'Saiba mais sobre: como converter cadeias de caracteres em uma matriz de bytes em Visual Basic'
title: Como converter cadeias de caracteres em uma matriz de bytes
ms.date: 07/20/2015
helpviewer_keywords:
- string conversion [Visual Basic], arrays
- arrays [Visual Basic], converting strings to
- byte arrays
- examples [Visual Basic], string conversion
- arrays [Visual Basic], byte arrays
ms.assetid: f477d35c-a3fc-4a30-b1d4-cd0d353aae1d
ms.openlocfilehash: edd41bc1dd7026c5b4ed061211f4b7884cd6044a
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100429839"
---
# <a name="how-to-convert-strings-into-an-array-of-bytes-in-visual-basic"></a>Como converter cadeias de caracteres em uma matriz de bytes no Visual Basic

Este tópico mostra como converter uma cadeia de caracteres em uma matriz de bytes.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa o <xref:System.Text.Encoding.GetBytes%2A> método da <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> classe Encoding para converter uma cadeia de caracteres em uma matriz de bytes.  
  
 [!code-vb[VbVbalrStrings#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#74)]  
  
 Você pode escolher entre várias opções de codificação para converter uma cadeia de caracteres em uma matriz de bytes:  
  
- <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType>: Obtém uma codificação para o conjunto de caracteres ASCII (7 bits).  
  
- <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=nameWithType>: Obtém uma codificação para o formato UTF-16 usando a ordem de bytes big-endian.  
  
- <xref:System.Text.Encoding.Default%2A?displayProperty=nameWithType>: Obtém uma codificação para a página de código ANSI atual do sistema.  
  
- <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType>: Obtém uma codificação para o formato UTF-16 usando a ordem de byte little-endian.  
  
- <xref:System.Text.Encoding.UTF32%2A?displayProperty=nameWithType>: Obtém uma codificação para o formato UTF-32 usando a ordem de byte little-endian.  
  
- <xref:System.Text.Encoding.UTF7%2A?displayProperty=nameWithType>: Obtém uma codificação para o formato UTF-7.  
  
- <xref:System.Text.Encoding.UTF8%2A?displayProperty=nameWithType>: Obtém uma codificação para o formato UTF-8.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Text.Encoding?displayProperty=nameWithType>
- <xref:System.Text.Encoding.GetBytes%2A>
- [Como converter uma matriz de bytes em uma cadeia de caracteres no Visual Basic](how-to-convert-an-array-of-bytes-into-a-string.md)
