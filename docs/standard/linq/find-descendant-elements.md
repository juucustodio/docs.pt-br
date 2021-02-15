---
title: Como localizar elementos descendentes-LINQ to XML
description: Este artigo mostra como usar o XPath e a consulta LINQ to XML, em C# e Visual Basic, para localizar todos os elementos descendentes que têm um nome especificado.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b318da39-bb8b-4c56-a019-e13b12b01831
ms.openlocfilehash: 36547c4ad39953e25bf7a8d5f69aa4a712e51982
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554228"
---
# <a name="how-to-find-descendant-elements-linq-to-xml"></a>Como localizar elementos descendentes (LINQ to XML)

Este artigo mostra como usar o XPath e a consulta LINQ to XML, em C# e Visual Basic, para localizar todos os elementos descendentes que têm um nome especificado.

## <a name="example-find-descendant-elements-that-have-a-specified-name"></a>Exemplo de localizar elementos descendentes que têm um nome especificado

 Este exemplo mostra como usar LINQ to XML consulta e o XPath para localizar todos os elementos descendentes nomeados `Name` no arquivo XML de exemplo de documento XML [: várias ordens de compra](sample-xml-file-multiple-purchase-orders.md). A expressão XPath é `//Name`.

```csharp
XDocument po = XDocument.Load("PurchaseOrders.xml");

// LINQ to XML query
IEnumerable<XElement> list1 = po.Root.Descendants("Name");

// XPath expression
IEnumerable<XElement> list2 = po.XPathSelectElements("//Name");

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = po...<Name>

' XPath expression
Dim list2 As IEnumerable(Of XElement) = po.XPathSelectElements("//Name")

If (list1.Count() = list2.Count() And _
        list1.Intersect(list2).Count() = list1.Count()) Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
For Each el As XElement In list1
    Console.WriteLine(el)
Next
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
<Name>Ellen Adams</Name>
<Name>Tai Yee</Name>
<Name>Cristian Osorio</Name>
<Name>Cristian Osorio</Name>
<Name>Jessica Arnold</Name>
<Name>Jessica Arnold</Name>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](./comparison-xpath-linq-xml.md)
