---
description: 'Saiba mais sobre: entrada de XPathDocument para XslTransform'
title: XPathDocument inseriu a XslTransform
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7d1bbe8b-ed43-4e62-a5ba-d602d244f4ae
ms.openlocfilehash: 5778a359cd4bfa748318533c9be6a1def97b5be3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782579"
---
# <a name="xpathdocument-input-to-xsltransform"></a>XPathDocument inseriu a XslTransform

<xref:System.Xml.XPath.XPathDocument> é um cache somente leitura, para processar documentos com <xref:System.Xml.Xsl.XslTransform>. Estruturalmente é semelhante ao modelo de objeto (DOM) de documento, mas altamente é otimizado para o idioma extensível de folha de estilos para transformações (XSLT) e processar o modelo de dados de idioma do caminho de XML (XPath) usando as funções de otimização XPath em <xref:System.Xml.XPath.XPathNavigator>.  
  
> [!NOTE]
> A classe <xref:System.Xml.Xsl.XslTransform> está obsoleta no .NET Framework 2.0. Você pode executar a linguagem XSL Transformations (XSLT) usando a classe <xref:System.Xml.Xsl.XslCompiledTransform>. Confira [Usar a classe XslCompiledTransform](using-the-xslcompiledtransform-class.md) e [Migrar da classe XslTransform](migrating-from-the-xsltransform-class.md) para saber mais.  
  
 O exemplo de código a seguir cria <xref:System.Xml.XPath.XPathDocument> como entrada uma transformação.  
  
```vb  
Dim xslt as XslTransform = new XslTransform()  
Xslt.Load(someStylesheet)  
Dim doc as XPathDocument = New XPathDocument("books.xml")  
Dim fs as StringWriter = new StringWriter()  
Xslt.Transform(doc, Nothing, fs, Nothing);  
```  
  
```csharp  
XslTransform xslt = new XslTransform();  
Xslt.Load(someStylesheet);  
XPathDocument doc = XPathDocument("books.xml");  
StringWriter fs = new StringWriter();  
Xslt.Transform(doc, null, fs, null);  
```  
  
## <a name="see-also"></a>Consulte também

- [A classe XslTransform implementa do processador XSLT](xsltransform-class-implements-the-xslt-processor.md)
