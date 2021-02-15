---
description: 'Saiba mais sobre: como converter um objeto em outro tipo em Visual Basic'
title: 'Como: Converter um objeto em outro tipo'
ms.date: 07/20/2015
helpviewer_keywords:
- objects [Visual Basic], converting
ms.assetid: 60cb5fc7-7ba4-4ab5-9c24-480fa12ddcdc
ms.openlocfilehash: d6840cfd440483720f8ca9a0fa0140c3727a8688
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100484022"
---
# <a name="how-to-convert-an-object-to-another-type-in-visual-basic"></a>Como converter um objeto em outro tipo no Visual Basic

Você converte uma `Object` variável em outro tipo de dados usando uma palavra-chave de conversão, como a [função CType](../../../language-reference/functions/ctype-function.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir converte uma `Object` variável em um `Integer` e um `String` .  
  
```vb  
Public Sub objectConversion(ByVal anObject As Object)  
    Dim anInteger As Integer  
    Dim aString As String  
    anInteger = CType(anObject, Integer)  
    aString = CType(anObject, String)  
End Sub  
```  
  
 Se você souber que o conteúdo de uma `Object` variável é de um tipo de dados específico, será melhor converter a variável para esse tipo de dados. Se você continuar usando a `Object` variável, você incorrerá em *Boxing* e *unboxing* (para um tipo de valor) ou *associação tardia* (para um tipo de referência). Todas essas operações têm tempo de execução extra e tornam o desempenho mais lento.  
  
## <a name="compile-the-code"></a>Compilar o código  

 Este exemplo requer:  
  
- Uma referência ao <xref:System?displayProperty=nameWithType> namespace.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Object>
- [Conversões de tipo no Visual Basic](type-conversions.md)
- [Conversões de Widening e Narrowing](widening-and-narrowing-conversions.md)
- [Conversões implícitas e explícitas](implicit-and-explicit-conversions.md)
- [Conversões entre cadeias de caracteres e outros tipos](conversions-between-strings-and-other-types.md)
- [Conversões de matriz](array-conversions.md)
- [Estruturas](structures.md)
- [Data Types](../../../language-reference/data-types/index.md)
- [Funções de conversão do tipo](../../../language-reference/functions/type-conversion-functions.md)
