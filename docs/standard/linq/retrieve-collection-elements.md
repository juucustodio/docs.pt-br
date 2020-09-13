---
title: Como recuperar uma coleção de elementos-LINQ to XML
description: Saiba como usar o método XContainer. Elements para recuperar uma coleção de elementos filho de um elemento.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b849668c-7976-4974-b8e1-1cd587d34258
ms.openlocfilehash: e73f608cff13f75f769f77372dc1c09949e00b0e
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551865"
---
# <a name="how-to-retrieve-a-collection-of-elements-linq-to-xml"></a>Como recuperar uma coleção de elementos (LINQ to XML)

Este artigo demonstra o <xref:System.Xml.Linq.XContainer.Elements%2A> método, que recupera uma coleção dos elementos filho de um elemento.

## <a name="example-iterate-through-the-child-elements-of-an-element"></a>Exemplo: iterar pelos elementos filho de um elemento

Este exemplo efetua iterações através dos elementos filho do elemento de `purchaseOrder` . Ele usa arquivo XML de exemplo de documento XML [: ordem de compra típica](sample-xml-file-typical-purchase-order.md).

```csharp
XElement po = XElement.Load("PurchaseOrder.xml");
IEnumerable<XElement> childElements =
    from el in po.Elements()
    select el;
foreach (XElement el in childElements)
    Console.WriteLine("Name: " + el.Name);
```

```vb
Dim po As XElement = XElement.Load("PurchaseOrder.xml")
Dim childElements As IEnumerable(Of XElement)
childElements = _
    From el In po.Elements() _
    Select el
For Each el As XElement In childElements
    Console.WriteLine("Name: " & el.Name.ToString())
Next
```

Esse exemplo gera a saída a seguir:

```output
Name: Address
Name: Address
Name: DeliveryNotes
Name: Items
```

## <a name="see-also"></a>Confira também

- [Visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md)
