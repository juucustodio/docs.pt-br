---
title: Como localizar irmãos precedentes-LINQ to XML
description: 'Saiba como localizar elementos irmãos que precedem um determinado elemento. Dois métodos são mostrados: um usa XPathSelectElements ao longo do eixo irmão precedente, o outro usa XNode. ElementsBeforeSelf.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b281ff99-d08a-43d0-bea1-eff831b2f8ae
ms.openlocfilehash: 788101eee6cdbce89626d1b46a5011a897c64704
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551941"
---
# <a name="how-to-find-preceding-siblings-linq-to-xml"></a>Como localizar irmãos precedentes (LINQ to XML)

Este artigo mostra como usar <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> ao longo do eixo irmão precedente para localizar elementos irmãos que precedem um determinado elemento e como usar <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType> para localizar os mesmos elementos.

## <a name="example-use-two-methods-to-find-sibling-elements-that-precede-an-element"></a>Exemplo: usar dois métodos para localizar elementos irmãos que precedem um elemento

O exemplo a seguir localiza o `FullAddress` elemento em arquivo XML de exemplo de documento XML [: Customers e Orders](sample-xml-file-customers-orders.md)e recupera os elementos irmãos precedentes de duas maneiras diferentes. Em seguida, ele compara os resultados e os encontra idênticos.

> [!NOTE]
> Os dois métodos fornecem resultados que estão na ordem do documento.

A expressão XPath usada é `preceding-sibling::*` .

```csharp
XElement co = XElement.Load("CustomersOrders.xml");

XElement add = co.Element("Customers").Element("Customer").Element("FullAddress");

// LINQ to XML query
IEnumerable<XElement> list1 = add.ElementsBeforeSelf();

// XPath expression
IEnumerable<XElement> list2 = add.XPathSelectElements("preceding-sibling::*");

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list2)
    Console.WriteLine(el);
```

```vb
Dim co As XElement = XElement.Load("CustomersOrders.xml")
Dim add As XElement = co.<Customers>.<Customer>. _
        <FullAddress>.FirstOrDefault

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = add.ElementsBeforeSelf()

' XPath expression
Dim list2 As IEnumerable(Of XElement) = add.XPathSelectElements("preceding-sibling::*")

If list1.Count() = list2.Count() And _
        list1.Intersect(list2).Count() = list1.Count() Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
For Each el As XElement In list2
    Console.WriteLine(el)
Next
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
<CompanyName>Great Lakes Food Market</CompanyName>
<ContactName>Howard Snyder</ContactName>
<ContactTitle>Marketing Manager</ContactTitle>
<Phone>(503) 555-7555</Phone>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
