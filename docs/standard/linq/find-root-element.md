---
title: Como localizar o elemento raiz-LINQ to XML
description: Saiba como usar XPath e LINQ to XML, em C# e Visual Basic, para localizar o elemento raiz de um documento XML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4fd824e0-4d39-429b-b092-f6a5c046ee6c
ms.openlocfilehash: 16217960b84276bd3bb4c5cb6b38d7cb56d2b41e
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551932"
---
# <a name="how-to-find-the-root-element-linq-to-xml"></a>Como localizar o elemento raiz (LINQ to XML)

Este artigo fornece um exemplo que mostra como usar XPath e LINQ to XML, em C# e Visual Basic, para localizar o elemento raiz de um documento XML.

## <a name="example-find-the-root-element"></a>Exemplo: localizar o elemento raiz

Este exemplo usa LINQ to XML consulta e XPath para localizar o elemento raiz no arquivo XML de exemplo de documento XML [: várias ordens de compra](sample-xml-file-multiple-purchase-orders.md). A expressão XPath é `/PurchaseOrders`.

```csharp
XDocument po = XDocument.Load("PurchaseOrders.xml");

// LINQ to XML query
XElement el1 = po.Root;

// XPath expression
XElement el2 = po.XPathSelectElement("/PurchaseOrders");

if (el1 == el2)
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
Console.WriteLine(el1.Name);
```

```vb
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")

' LINQ to XML query
Dim el1 As XElement = po.Root

' XPath expression
Dim el2 As XElement = po.XPathSelectElement("/PurchaseOrders")

If el1 Is el2 Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
Console.WriteLine(el1.Name)
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
PurchaseOrders
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](/../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
