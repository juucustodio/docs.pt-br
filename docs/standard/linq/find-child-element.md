---
title: Como encontrar um elemento filho-LINQ to XML
description: Este artigo compara o eixo de elemento filho XPath com o <xref:System.Xml.Linq.XContainer.Element%2A> método LINQ to XML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4fa6182d-6196-4ed1-9c9e-82949ff89c71
ms.openlocfilehash: 34ddfd78489927a40128196a6fc80e822302428b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557124"
---
# <a name="how-to-find-a-child-element-linq-to-xml"></a>Como localizar um elemento filho (LINQ to XML)

Este artigo compara o eixo de elemento filho XPath com o <xref:System.Xml.Linq.XContainer.Element%2A> método LINQ to XML.

## <a name="example-find-a-child-element-in-an-xml-document"></a>Exemplo: localizar um elemento filho em um documento XML

Este exemplo localiza o elemento filho `DeliveryNotes` no arquivo XML de exemplo de documento XML [: várias ordens de compra](sample-xml-file-multiple-purchase-orders.md).

A expressão XPath é `DeliveryNotes`.

```csharp
XDocument cpo = XDocument.Load("PurchaseOrders.xml");
XElement po = cpo.Root.Element("PurchaseOrder");

// LINQ to XML query
XElement el1 = po.Element("DeliveryNotes");

// XPath expression
XElement el2 = po.XPathSelectElement("DeliveryNotes");
// same as "child::DeliveryNotes"
// same as "./DeliveryNotes"

if (el1 == el2)
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
Console.WriteLine(el1);
```

```vb
Dim cpo As XDocument = XDocument.Load("PurchaseOrders.xml")
Dim po As XElement = cpo.Root.<PurchaseOrder>.FirstOrDefault

'LINQ to XML query
Dim el1 As XElement = po.<DeliveryNotes>.FirstOrDefault

' XPath expression
Dim el2 As XElement = po.XPathSelectElement("DeliveryNotes")
' same as "child::DeliveryNotes"
' same as "./DeliveryNotes"

If el1 Is el2 Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
Console.WriteLine(el1)
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
<DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](./comparison-xpath-linq-xml.md)
