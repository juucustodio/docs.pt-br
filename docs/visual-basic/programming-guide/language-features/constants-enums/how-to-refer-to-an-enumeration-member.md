---
description: 'Saiba mais sobre: como fazer: referência a um membro de enumeração (Visual Basic)'
title: Como fazer referência a um membro de enumeração
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic], referring to
- values [Visual Basic], associating constant values with names
- enumeration members
- constants [Visual Basic], enumerated
ms.assetid: bbb5c3cc-7cdb-4814-8d6a-a6d91546ed1e
ms.openlocfilehash: 339ea8292eea1b39e2c6e5879b98a083800fb1fc
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100471520"
---
# <a name="how-to-refer-to-an-enumeration-member-visual-basic"></a>Como fazer referência a um membro de enumeração (Visual Basic)

As enumerações fornecem uma maneira conveniente de trabalhar com conjuntos de constantes relacionadas e associar valores constantes a nomes. Por exemplo, é possível declarar uma enumeração de um conjunto de constantes de inteiros associados aos dias da semana e, em seguida, usar os nomes de dias em vez de seus valores de inteiros em seu código.  
  
 Você pode evitar o uso de nomes totalmente qualificados com a `Imports` instrução. Para obter mais informações, consulte [enumerações e qualificação de nome](enumerations-and-name-qualification.md).  
  
### <a name="to-refer-to-an-enumeration-member"></a>Para fazer referência a um membro de enumeração  
  
- Qualifique o nome do membro com a enumeração. Por exemplo, o exemplo a seguir atribui o `Saturday` membro da `FirstDayOfWeek` Enumeração à variável `DayValue` .  
  
     [!code-vb[VbEnumsTask#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#19)]  
  
## <a name="see-also"></a>Consulte também

- [Como declarar uma enumeração](how-to-declare-enumerations.md)
- [Enumerações e qualificação de nome](enumerations-and-name-qualification.md)
- [Como iterar em uma enumeração no Visual Basic](how-to-iterate-through-an-enumeration.md)
- [Como determinar a cadeia de caracteres associada a um valor de enumeração](how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [Quando usar uma enumeração](when-to-use-an-enumeration.md)
