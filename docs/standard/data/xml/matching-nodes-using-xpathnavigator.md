---
description: 'Saiba mais sobre: nós correspondentes usando XPathNavigator'
title: Nós compatíveis usando XPathNavigator
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e6848c47-ee5d-401a-89a5-50b5eed40f30
ms.openlocfilehash: d142490829473d0891c5b2f18b1c3ec9e7ace426
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732001"
---
# <a name="matching-nodes-using-xpathnavigator"></a>Nós compatíveis usando XPathNavigator

A classe de <xref:System.Xml.XPath.XPathNavigator> fornece o método de <xref:System.Xml.XPath.XPathNavigator.Matches%2A> para determinar se um nó corresponde uma expressão XPath. O método de <xref:System.Xml.XPath.XPathNavigator.Matches%2A> usa uma expressão XPath como entrada e retorna <xref:System.Boolean> que indica se o nó atual corresponde a expressão XPath determinada ou o objeto compilado dado de <xref:System.Xml.XPath.XPathExpression> .  
  
## <a name="matching-nodes"></a>Nós compatíveis  

 O método de <xref:System.Xml.XPath.XPathNavigator.Matches%2A> retorna `true` se o nó atual corresponde a expressão XPath especificada. Por exemplo, no exemplo de código que segue, o método de <xref:System.Xml.XPath.XPathNavigator.Matches%2A> retornará `true` se o nó atual é o elemento `b`, e o elemento `b` tem um atributo `c`.  
  
> [!NOTE]
> O método de <xref:System.Xml.XPath.XPathNavigator.Matches%2A> não altera o estado de <xref:System.Xml.XPath.XPathNavigator>.  
  
```vb  
Dim document as XPathDocument = New XPathDocument("input.xml")  
Dim navigator as XPathNavigator = document.CreateNavigator()  
  
navigator.Matches("b[@c]")  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.Matches("b[@c]");  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [Processar dados XML usando o modelo de dados XPath](process-xml-data-using-the-xpath-data-model.md)
- [Selecionar dados XML usando XPathNavigator](select-xml-data-using-xpathnavigator.md)
- [Avalia as expressões XPath usando XPathNavigator](evaluate-xpath-expressions-using-xpathnavigator.md)
- [Tipos de nós reconhecidos com consultas XPath](node-types-recognized-with-xpath-queries.md)
- [Consultas XPath e namespaces](xpath-queries-and-namespaces.md)
- [Expressões XPath compilados](compiled-xpath-expressions.md)
