---
title: Como calcular valores intermediários-LINQ to XML
description: Calcule valores intermediários para uso em classificação, filtragem e seleção.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 7fd3001f-f8f9-4bce-879f-d4c7af8a04fe
ms.openlocfilehash: c37926b93e0dc11255fd27c312679f6286fa7e5d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558114"
---
# <a name="how-to-calculate-intermediate-values-linq-to-xml"></a>Como calcular valores intermediários (LINQ to XML)

Este artigo mostra como calcular valores intermediários para uso em classificação, filtragem e seleção em C# e Visual Basic.

## <a name="example-use-the-let-clause-to-calculate-based-on-element-data"></a>Exemplo: Use a `let` cláusula para calcular com base nos dados do elemento

O exemplo a seguir usa a `let` cláusula para calcular produtos de valores numéricos de elementos. Ele usa arquivo XML de exemplo de documento XML [: dados numéricos](sample-xml-file-numerical-data.md).

```csharp
XElement root = XElement.Load("Data.xml");
IEnumerable<decimal> extensions =
    from el in root.Elements("Data")
    let extension = (decimal)el.Element("Quantity") * (decimal)el.Element("Price")
    where extension >= 25
    orderby extension
    select extension;
foreach (decimal ex in extensions)
    Console.WriteLine(ex);
```

```vb
Dim root As XElement = XElement.Load("Data.xml")
Dim extensions As IEnumerable(Of Decimal) = _
    From el In root.<Data> _
    Let extension = CDec(el.<Quantity>.Value) * CDec(el.<Price>.Value) _
    Where extension > 25 _
    Order By extension _
    Select extension
For Each ex As Decimal In extensions
    Console.WriteLine(ex)
Next
```

Esse exemplo gera a saída a seguir:

```output
55.92
73.50
89.99
198.00
435.00
```

## <a name="example-calculate-from-xml-thats-in-a-namespace"></a>Exemplo: calcular do XML que está em um namespace

O exemplo a seguir mostra a mesma consulta que antes, mas para XML que está em um namespace. Ele usa o arquivo XML de exemplo de documento XML [: dados numéricos em um namespace](sample-xml-file-numerical-data-namespace.md).

Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

```csharp
XElement root = XElement.Load("DataInNamespace.xml");
XNamespace ad = "http://www.adatum.com";
IEnumerable<decimal> extensions =
    from el in root.Elements(ad + "Data")
    let extension = (decimal)el.Element(ad + "Quantity") * (decimal)el.Element(ad + "Price")
    where extension >= 25
    orderby extension
    select extension;
foreach (decimal ex in extensions)
    Console.WriteLine(ex);
```

```vb
Imports <xmlns="http://www.adatum.com">

Module Module1
    Sub Main()
        Dim root As XElement = XElement.Load("DataInNamespace.xml")
        Dim extensions As IEnumerable(Of Decimal) = _
            From el In root.<Data> _
            Let extension = CDec(el.<Quantity>.Value) * CDec(el.<Price>.Value) _
            Where extension > 25 _
            Order By extension _
            Select extension
        For Each ex As Decimal In extensions
            Console.WriteLine(ex)
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
55.92
73.50
89.99
198.00
435.00
```

## <a name="see-also"></a>Confira também

- [Consultas básicas (LINQ to XML) (Visual Basic)](./find-element-specific-attribute.md)
