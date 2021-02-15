---
title: Como determinar a cadeia de caracteres associada a um valor de enumeração
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic]
- strings [Visual Basic], enumeration values
- values [Visual Basic], enumeration members
ms.assetid: 9253e7c8-579c-49a2-8f26-392b20ea99eb
ms.openlocfilehash: 4138759bfbb049b77406fc536219b40d3ed9e2a5
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91058763"
---
# <a name="how-to-determine-the-string-associated-with-an-enumeration-value-visual-basic"></a>Como determinar a cadeia de caracteres associada a um valor de enumeração (Visual Basic)

Os <xref:System.Enum.GetValues%2A> <xref:System.Enum.GetNames%2A> métodos e permitem que você determine as cadeias de caracteres e os valores associados aos membros da enumeração.  
  
### <a name="to-determine-the-string-associated-with-an-enumeration"></a>Para determinar a cadeia de caracteres associada a uma enumeração  
  
- Use o <xref:System.Enum.GetNames%2A> método para recuperar as cadeias de caracteres associadas aos membros da enumeração. Este exemplo declara uma enumeração, e, `flavorEnum` em seguida, usa o <xref:System.Enum.GetNames%2A> método para exibir as cadeias de caracteres associadas a cada membro.  
  
     [!code-vb[VbEnumsTask#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#2)]  
  
## <a name="see-also"></a>Confira também

- <xref:System.Enum.GetValues%2A>
- <xref:System.Enum.GetNames%2A>
- <xref:System.Enum>
- [Como declarar uma enumeração](how-to-declare-enumerations.md)
- [Como fazer referência a um membro de enumeração](how-to-refer-to-an-enumeration-member.md)
- [Enumerações e qualificação de nome](enumerations-and-name-qualification.md)
- [Como iterar em uma enumeração no Visual Basic](how-to-iterate-through-an-enumeration.md)
- [Quando usar uma enumeração](when-to-use-an-enumeration.md)
- [Instrução Enum](../../../language-reference/statements/enum-statement.md)
