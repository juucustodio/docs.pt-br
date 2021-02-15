---
description: 'Saiba mais sobre: como iterar por meio de uma enumeração no Visual Basic'
title: Como iterar em uma enumeração
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [Visual Basic], iterating
- enumerations [Visual Basic], iterating
- ListBox control [Windows Forms], populating from an enumeration
ms.assetid: e5aa10eb-cfcd-4a3b-8e76-f06b8f2002be
ms.openlocfilehash: a14d65a33e8a2f7872203a6a332dec1e753704f8
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100471559"
---
# <a name="how-to-iterate-through-an-enumeration-in-visual-basic"></a>Como iterar em uma enumeração no Visual Basic

Enumerações fornecem uma maneira conveniente para trabalhar com conjuntos de constantes relacionadas e para associar valores de constante a nomes. Para iterar por meio de uma enumeração, você pode movê-lo para uma matriz usando o <xref:System.Enum.GetValues%2A> método. Você também pode iterar por meio de uma enumeração usando uma `For...Each` instrução, usando o <xref:System.Enum.GetNames%2A> <xref:System.Enum.GetValues%2A> método ou para extrair a cadeia de caracteres ou o valor numérico.  
  
### <a name="to-iterate-through-an-enumeration"></a>Para iterar por meio de uma enumeração  
  
- Declare uma matriz e converta a enumeração para ela com o <xref:System.Enum.GetValues%2A> método antes de passar a matriz, como faria com qualquer outra variável. O exemplo a seguir exibe cada membro da enumeração <xref:Microsoft.VisualBasic.FirstDayOfWeek> à medida que ele é iterado pela enumeração.  
  
     [!code-vb[VbEnumsTask#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#7)]  
  
## <a name="see-also"></a>Consulte também

- [Visão geral de enumerações](enumerations-overview.md)
- [Como declarar uma enumeração](how-to-declare-enumerations.md)
- [Quando usar uma enumeração](when-to-use-an-enumeration.md)
- [Como determinar a cadeia de caracteres associada a um valor de enumeração](how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [Como fazer referência a um membro de enumeração](how-to-refer-to-an-enumeration-member.md)
- [Enumerações e qualificação de nome](enumerations-and-name-qualification.md)
- [matrizes](../arrays/index.md)
