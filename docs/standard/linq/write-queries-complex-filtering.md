---
title: Como escrever consultas com filtragem complexa-LINQ to XML
description: Muitas vezes, você deseja escrever consultas LINQ to XML com filtros complexos. Por exemplo, você pode ter que localizar todos os elementos que têm um elemento filho com um nome e um valor específicos.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4065d901-cf89-4e47-8bf9-abb65acfb003
ms.openlocfilehash: c5e7f812364e7e96e3a4b8f5515d07a3524ec979
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552317"
---
# <a name="how-to-write-queries-with-complex-filtering-linq-to-xml"></a>Como escrever consultas com filtragem complexa (LINQ to XML)

Muitas vezes, você deseja escrever consultas LINQ to XML com filtros complexos. Por exemplo, você pode ter que localizar todos os elementos que têm um elemento filho com um nome e um valor específicos. Este artigo fornece um exemplo de como escrever uma consulta com filtragem complexa.

## <a name="example-find-with-a-nested-query-in-the-where-clause"></a>Exemplo: localizar com uma consulta aninhada na `Where` cláusula

Este exemplo mostra como localizar todos os `PurchaseOrder` elementos que têm:

- Um `Address` elemento filho cujo `Type` atributo é igual a "Shipping".
- Um `State` elemento filho que é igual a "NY".

Ele usa uma consulta aninhada na cláusula `Where` e o operador `Any` retornará `true` se a coleção tiver elementos nele. O exemplo usa arquivo XML de exemplo de documento XML [: várias ordens de compra](sample-xml-file-multiple-purchase-orders.md).

Para obter mais informações sobre o `Any` operador, consulte [operações do quantificador (C#)](../../../docs/csharp/programming-guide/concepts/linq/quantifier-operations.md) e [operações do quantificador (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md).

```csharp
XElement root = XElement.Load("PurchaseOrders.xml");
IEnumerable<XElement> purchaseOrders =
    from el in root.Elements("PurchaseOrder")
    where
        (from add in el.Elements("Address")
        where
            (string)add.Attribute("Type") == "Shipping" &&
            (string)add.Element("State") == "NY"
        select add)
        .Any()
    select el;
foreach (XElement el in purchaseOrders)
    Console.WriteLine((string)el.Attribute("PurchaseOrderNumber"));
```

```vb
Dim root As XElement = XElement.Load("PurchaseOrders.xml")
Dim purchaseOrders As IEnumerable(Of XElement) = _
    From el In root.<PurchaseOrder> _
    Where _
        (From add In el.<Address> _
        Where _
             add.@Type = "Shipping" And _
             add.<State>.Value = "NY" _
        Select add) _
    .Any() _
    Select el
For Each el As XElement In purchaseOrders
    Console.WriteLine(el.@PurchaseOrderNumber)
Next
```

Esse exemplo gera a saída a seguir:

```output
99505
```

## <a name="example-find-in-xml-thats-in-a-namespace"></a>Exemplo: Localizar em XML que está em um namespace

O exemplo a seguir mostra a mesma consulta como acima, mas para XML que está em um namespace. Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

Este exemplo usa arquivo XML de exemplo de documento XML [: várias ordens de compra em um namespace](sample-xml-file-multiple-purchase-orders-namespace.md).

```csharp
XElement root = XElement.Load("PurchaseOrdersInNamespace.xml");
XNamespace aw = "http://www.adventure-works.com";
IEnumerable<XElement> purchaseOrders =
    from el in root.Elements(aw + "PurchaseOrder")
    where
        (from add in el.Elements(aw + "Address")
         where
             (string)add.Attribute(aw + "Type") == "Shipping" &&
             (string)add.Element(aw + "State") == "NY"
         select add)
        .Any()
    select el;
foreach (XElement el in purchaseOrders)
    Console.WriteLine((string)el.Attribute(aw + "PurchaseOrderNumber"));
```

```vb
Imports <xmlns:aw='http://www.adventure-works.com'>

Module Module1
    Sub Main()
        Dim root As XElement = XElement.Load("PurchaseOrdersInNamespace.xml")
        Dim purchaseOrders As IEnumerable(Of XElement) = _
            From el In root.<aw:PurchaseOrder> _
            Where _
                (From add In el.<aw:Address> _
                Where _
                     add.@aw:Type = "Shipping" And _
                     add.<aw:State>.Value = "NY" _
                Select add) _
            .Any() _
            Select el
        For Each el As XElement In purchaseOrders
            Console.WriteLine(el.@aw:PurchaseOrderNumber)
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
99505
```

## <a name="see-also"></a>Confira também

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [Operações de projeção (C#)](../../csharp/programming-guide/concepts/linq/projection-operations.md)
- [Operações de quantificador (C#)](../../csharp/programming-guide/concepts/linq/quantifier-operations.md)
- [Propriedade do eixo filho XML (Visual Basic)](../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)
- [Propriedade de eixo do atributo XML (Visual Basic)](../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)
- [Propriedade do valor XML (Visual Basic)](../../visual-basic/language-reference/xml-axis/xml-value-property.md)
- [Operações de projeção (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/projection-operations.md)
- [Operações do quantificador (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md)
