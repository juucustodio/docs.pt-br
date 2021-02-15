---
description: 'Saiba mais sobre: como acessar elementos filho XML (Visual Basic)'
title: Como acessar elementos filho XML
ms.date: 07/20/2015
helpviewer_keywords:
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 6689eb36-c471-469f-a82d-099ab8197b25
ms.openlocfilehash: fad4d45853006762bc319b0ff8f9143ef13058da
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100433233"
---
# <a name="how-to-access-xml-child-elements-visual-basic"></a>Como acessar elementos filho XML (Visual Basic)

Este exemplo mostra como usar uma propriedade de eixo filho para acessar todos os elementos filho XML que têm um nome especificado em um elemento XML. Em particular, ele usa a <xref:System.Xml.Linq.XElement.Value%2A> propriedade para obter o valor do primeiro elemento na coleção que a propriedade do `name` eixo filho retorna. A `name` Propriedade do eixo filho obtém todos os elementos filho chamados `phone` no `contact` objeto. Este exemplo também usa a `phone` propriedade de eixo filho para acessar todos os elementos filho chamados `phone` que estão contidos no `contact` objeto.  
  
## <a name="example"></a>Exemplo  

 [!code-vb[VbXMLSamples#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples4.vb#10)]  
  
## <a name="compile-the-code"></a>Compilar o código  

 Este exemplo requer:  
  
- Uma referência ao <xref:System.Xml.Linq> namespace.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>
- [Propriedade do Eixo Filho XML](../../../language-reference/xml-axis/xml-child-axis-property.md)
- [Propriedade do Valor XML](../../../language-reference/xml-axis/xml-value-property.md)
- [Acessando XML no Visual Basic](accessing-xml.md)
- [XML](index.md)
