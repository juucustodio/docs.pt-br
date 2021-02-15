---
description: 'Saiba mais sobre: acesso de cadeia de caracteres baseado em zero vs. uma com base em um Visual Basic'
title: Acesso de cadeia de caracteres baseado em zero versus um
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], indexing
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
ms.openlocfilehash: adab6954c4329ae0a547d136f26f6c3115dc5890
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100463826"
---
# <a name="zero-based-vs-one-based-string-access-in-visual-basic"></a>Acesso à cadeia de caracteres com base em zero versus em um no Visual Basic

Este tópico compara como Visual Basic e o .NET Framework fornecem acesso aos caracteres em uma cadeia de caracteres. O .NET Framework sempre fornece acesso baseado em zero aos caracteres em uma cadeia de caracteres, enquanto Visual Basic fornece acesso baseado em zero e um baseado em um, dependendo da função.  
  
## <a name="one-based"></a>One-Based  

 Para obter um exemplo de uma função de Visual Basic baseada em um, considere a `Mid` função. Ele usa um argumento que indica a posição do caractere na qual a subcadeia de caracteres será iniciada, começando com a posição 1. O <xref:System.String.Substring%2A?displayProperty=nameWithType> método .NET Framework usa um índice do caractere na cadeia de caracteres na qual a subcadeia de caracteres é iniciada, começando com a posição 0. Portanto, se você tiver uma cadeia de caracteres "ABCDE", os caracteres individuais serão numerados como 1, 2, 3, 4, 5 para uso com a `Mid` função, mas 0, 1, 2, 3, 4 para uso com o <xref:System.String.Substring%2A?displayProperty=nameWithType> método.  
  
## <a name="zero-based"></a>Zero-Based  

 Para obter um exemplo de uma função de Visual Basic com base em zero, considere a `Split` função. Ele divide uma cadeia de caracteres e retorna uma matriz que contém as subcadeias de caracteres. O <xref:System.String.Split%2A?displayProperty=nameWithType> método .NET Framework também divide uma cadeia de caracteres e retorna uma matriz que contém as subcadeias de caracteres. Como a `Split` função e o <xref:System.String.Split%2A> método retornam .NET Framework matrizes, eles devem ser baseados em zero.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Strings.Mid%2A>
- <xref:Microsoft.VisualBasic.Strings.Split%2A>
- <xref:System.String.Substring%2A>
- <xref:System.String.Split%2A>
- [Introdução a cadeias de caracteres no Visual Basic](introduction-to-strings.md)
