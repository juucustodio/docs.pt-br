---
title: Como recuperar uma coleção de atributos-LINQ to XML
description: Saiba como usar o método XElement. Attributes para recuperar os atributos de um elemento.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: a49ee7a3-b2c2-4d49-9b5c-b7c6c41f4f13
ms.openlocfilehash: a15375ffd6b3af7fb9119e3321495cffa00268e4
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551902"
---
# <a name="how-to-retrieve-a-collection-of-attributes-linq-to-xml"></a>Como recuperar uma coleção de atributos (LINQ to XML)

Este artigo mostra o uso do <xref:System.Xml.Linq.XElement.Attributes%2A> método para recuperar os atributos de um elemento.

## <a name="example-iterate-through-the-attributes-of-an-element"></a>Exemplo: iterar pelos atributos de um elemento

O exemplo a seguir mostra como iterar através da coleção de atributos de um elemento.

```csharp
XElement val = new XElement("Value",
    new XAttribute("ID", "1243"),
    new XAttribute("Type", "int"),
    new XAttribute("ConvertableTo", "double"),
    "100");
IEnumerable<XAttribute> listOfAttributes =
    from att in val.Attributes()
    select att;
foreach (XAttribute a in listOfAttributes)
    Console.WriteLine(a);
```

```vb
Dim val = _
    <Value ID="1243" Type="int" ConvertableTo="double">100</Value>
Dim listOfAttributes As IEnumerable(Of XAttribute) = _
    From att In val.Attributes() _
    Select att
For Each att As XAttribute In listOfAttributes
    Console.WriteLine(att)
Next
```

Esse exemplo gera a saída a seguir:

```output
ID="1243"
Type="int"
ConvertableTo="double"
```

## <a name="see-also"></a>Confira também

- [Visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md)
