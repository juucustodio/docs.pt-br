---
title: Como recuperar um único elemento filho-LINQ to XML
description: Recupere o primeiro elemento filho que tem um nome especificado. Você pode usar XContainer. Element em C# e a notação do indexador de matriz no Visual Basic.
ms.date: 07/20/2015
ms.assetid: ce37db9e-76fa-46eb-b4cc-e8f32d22ad90
ms.openlocfilehash: e557e82e4e5891d6890a0efb4973796050b75349
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552058"
---
# <a name="how-to-retrieve-a-single-child-element-linq-to-xml"></a>Como recuperar um único elemento filho (LINQ to XML)

Este artigo explica como recuperar um único elemento filho, o primeiro elemento filho que tem um nome especificado. No C#, você faz isso com o <xref:System.Xml.Linq.XContainer.Element%2A> método. No Visual Basic você faz isso com a notação do indexador de matriz.

## <a name="example-retrieve-the-first-element-that-has-a-specified-name"></a>Exemplo: recuperar o primeiro elemento que tem um nome especificado

O exemplo a seguir recupera o primeiro `DeliveryNotes` elemento do documento XML no [arquivo XML de exemplo: ordem de compra típica](sample-xml-file-typical-purchase-order.md).

```csharp
XElement po = XElement.Load("PurchaseOrder.xml");
XElement e = po.Element("DeliveryNotes");
Console.WriteLine(e);
```

```vb
Dim po As XElement = XElement.Load("PurchaseOrder.xml")
Dim e As XElement = po.<DeliveryNotes>(0)
Console.WriteLine(e)
```

Esse exemplo gera a saída a seguir:

```xml
<DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>
```

## <a name="example-retrieve-from-xml-thats-in-a-namespace"></a>Exemplo: recuperar do XML que está em um namespace

O exemplo a seguir faz a mesma coisa que a acima, mas para XML que está em um namespace. Ele usa o arquivo XML de exemplo de documento XML [: ordem de compra típica em um namespace](sample-xml-file-typical-purchase-order-namespace.md). Para obter mais informações sobre namespaces, consulte [visão geral de namespaces](namespaces-overview.md).

```csharp
XElement po = XElement.Load("PurchaseOrderInNamespace.xml");
XNamespace aw = "http://www.adventure-works.com";
XElement e = po.Element(aw + "DeliveryNotes");
Console.WriteLine(e);
```

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim po As XElement = XElement.Load("PurchaseOrderInNamespace.xml")
        Dim e As XElement = po.<aw:DeliveryNotes>(0)
        Console.WriteLine(e)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```xml
<aw:DeliveryNotes xmlns:aw="http://www.adventure-works.com">Please leave packages in shed by driveway.</aw:DeliveryNotes>
```

## <a name="see-also"></a>Confira também

- [Visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md)
