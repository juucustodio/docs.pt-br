---
title: Como localizar uma lista de elementos filho-LINQ to XML
description: Este artigo compara o eixo dos elementos filho do XPath com o eixo LINQ to XML XContainer. Elements.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 7c589dd8-f680-4cdb-9d6a-78d57e2555e8
ms.openlocfilehash: c575df2e8caa2125091265c00557b91a24601e48
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90549594"
---
# <a name="how-to-find-a-list-of-child-elements-linq-to-xml"></a>Como localizar uma lista de elementos filho (LINQ to XML)

Este artigo compara o eixo dos elementos filho do XPath com o eixo de LINQ to XML <xref:System.Xml.Linq.XContainer.Elements%2A> .

## <a name="example-find-all-child-elements-of-an-element"></a>Exemplo: localizar todos os elementos filho de um elemento

Este exemplo localiza todos os elementos filho do `Address` elemento no [arquivo XML de exemplo documento XML: várias ordens de compra](sample-xml-file-multiple-purchase-orders.md).

A expressão XPath é: `./*`

```csharp
XDocument cpo = XDocument.Load("PurchaseOrders.xml");
XElement po = cpo.Root.Element("PurchaseOrder").Element("Address");

// LINQ to XML query
IEnumerable<XElement> list1 = po.Elements();

// XPath expression
IEnumerable<XElement> list2 = po.XPathSelectElements("./*");

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim cpo As XDocument = XDocument.Load("PurchaseOrders.xml")
Dim po As XElement = cpo.Root.<PurchaseOrder>.<Address>.FirstOrDefault

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = po.Elements()

' XPath expression
Dim list2 As IEnumerable(Of XElement) = po.XPathSelectElements("./*")

If (list1.Count() = list2.Count()) AndAlso _
    (list1.Intersect(list2).Count() = list1.Count()) Then
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
<Street>123 Maple Street</Street>
<City>Mill Valley</City>
<State>CA</State>
<Zip>10999</Zip>
<Country>USA</Country>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](./comparison-xpath-linq-xml.md)
