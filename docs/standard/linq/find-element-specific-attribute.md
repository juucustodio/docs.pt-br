---
title: Como localizar um elemento com um atributo específico-LINQ to XML
description: Saiba como localizar um elemento cujo atributo tem um valor específico.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b92591aa-3cfb-490e-99f6-da8de335e362
ms.openlocfilehash: 4c74de90a348d81ac87c98bf6ee27f3c78f34e83
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551835"
---
# <a name="how-to-find-an-element-with-a-specific-attribute-linq-to-xml"></a>Como localizar um elemento com um atributo específico (LINQ to XML)

Este artigo fornece exemplos de como encontrar um elemento cujo atributo tem um valor específico.

## <a name="example-find-an-element-whose-attribute-has-a-specific-value"></a>Exemplo: localizar um elemento cujo atributo tem um valor específico

O exemplo a seguir mostra como localizar o `Address` elemento que tem um `Type` atributo com um valor de "cobrança". O exemplo usa arquivo XML de exemplo de documento XML [: ordem de compra típica](sample-xml-file-typical-purchase-order.md).

```csharp
XElement root = XElement.Load("PurchaseOrder.xml");
IEnumerable<XElement> address =
    from el in root.Elements("Address")
    where (string)el.Attribute("Type") == "Billing"
    select el;
foreach (XElement el in address)
    Console.WriteLine(el);
```

```vb
Dim root As XElement = XElement.Load("PurchaseOrder.xml")
Dim address As IEnumerable(Of XElement) = _
    From el In root.<Address> _
    Where el.@Type = "Billing" _
    Select el
For Each el As XElement In address
    Console.WriteLine(el)
Next
```

Esse exemplo gera a saída a seguir:

```xml
<Address Type="Billing">
  <Name>Tai Yee</Name>
  <Street>8 Oak Avenue</Street>
  <City>Old Town</City>
  <State>PA</State>
  <Zip>95819</Zip>
  <Country>USA</Country>
</Address>
```

## <a name="example-find-an-element-in-xml-thats-in-a-namespace"></a>Exemplo: localizar um elemento em XML que está em um namespace

O exemplo a seguir mostra a mesma consulta, mas para XML que está em um namespace. Ele usa [arquivo XML de exemplo de documento XML: ordem de compra típica em um namespace](sample-xml-file-typical-purchase-order-namespace.md).

Para obter mais informações sobre namespaces, consulte [visão geral de namespaces](namespaces-overview.md).

```csharp
XElement root = XElement.Load("PurchaseOrderInNamespace.xml");
XNamespace aw = "http://www.adventure-works.com";
IEnumerable<XElement> address =
    from el in root.Elements(aw + "Address")
    where (string)el.Attribute(aw + "Type") == "Billing"
    select el;
foreach (XElement el in address)
    Console.WriteLine(el);
```

```vb
Imports <xmlns:aw='http://www.adventure-works.com'>

Module Module1
    Sub Main()
        Dim root As XElement = XElement.Load("PurchaseOrderInNamespace.xml")
        Dim address As IEnumerable(Of XElement) = _
            From el In root.<aw:Address> _
            Where el.@aw:Type = "Billing" _
            Select el
        For Each el As XElement In address
            Console.WriteLine(el)
        Next
    End Sub
End Module
```

Este exemplo produz a seguinte saída::

```xml
<aw:Address aw:Type="Billing" xmlns:aw="http://www.adventure-works.com">
  <aw:Name>Tai Yee</aw:Name>
  <aw:Street>8 Oak Avenue</aw:Street>
  <aw:City>Old Town</aw:City>
  <aw:State>PA</aw:State>
  <aw:Zip>95819</aw:Zip>
  <aw:Country>USA</aw:Country>
</aw:Address>
```

## <a name="see-also"></a>Confira também

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [Visão geral de operadores de consulta padrão (C#)](../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Operações de projeção (C#)](../../csharp/programming-guide/concepts/linq/projection-operations.md)
- [Consultas básicas (LINQ to XML) (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
- [Visão geral de operadores de consulta padrão (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Operações de projeção (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/projection-operations.md)
