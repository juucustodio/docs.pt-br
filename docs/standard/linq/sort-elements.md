---
title: Como classificar elementos-LINQ to XML
description: Saiba como escrever uma consulta que classifica seus resultados.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: aee6fbbc-81fd-4b3e-b40f-6ed7b3bd3fee
ms.openlocfilehash: 0e93add12e39c71c7312036917d42dd53450b712
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90550065"
---
# <a name="how-to-sort-elements-linq-to-xml"></a>Como classificar elementos (LINQ to XML)

Você pode classificar seus resultados ao consultar XML. Este artigo fornece dois exemplos: o primeiro classifica os resultados de XML que *não estão* em um namespace e o segundo faz a mesma classificação, mas para XML que *está* em um namespace.

## <a name="example-write-a-query-that-sorts-its-results"></a>Exemplo: escrever uma consulta que classifica seus resultados

Este exemplo mostra como escrever uma consulta que classifica seus resultados. Ele usa arquivo XML de exemplo de documento XML [: dados numéricos](sample-xml-file-numerical-data.md).

```csharp
XElement root = XElement.Load("Data.xml");
IEnumerable<decimal> prices =
    from el in root.Elements("Data")
    let price = (decimal)el.Element("Price")
    orderby price
    select price;
foreach (decimal el in prices)
    Console.WriteLine(el);
```

```vb
Dim root As XElement = XElement.Load("Data.xml")
Dim prices As IEnumerable(Of Decimal) = _
    From el In root.<Data> _
    Let price = Convert.ToDecimal(el.<Price>.Value) _
    Order By (price) _
    Select price
For Each el As Decimal In prices
    Console.WriteLine(el)
Next
```

Esse exemplo gera a saída a seguir:

```output
0.99
4.95
6.99
24.50
29.00
66.00
89.99
```

## <a name="example-write-a-query-in-a-namespace-that-sorts-its-results"></a>Exemplo: gravar uma consulta em um namespace que classifica seus resultados

O exemplo a seguir mostra a mesma consulta para XML que está em um namespace. Ele usa [arquivo XML de exemplo de documento XML: dados numéricos em um namespace](sample-xml-file-numerical-data-namespace.md).

Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

```csharp
XElement root = XElement.Load("DataInNamespace.xml");
XNamespace aw = "http://www.adatum.com";
IEnumerable<decimal> prices =
    from el in root.Elements(aw + "Data")
    let price = (decimal)el.Element(aw + "Price")
    orderby price
    select price;
foreach (decimal el in prices)
    Console.WriteLine(el);
```

```vb
Imports <xmlns='http://www.adatum.com'>

Module Module1
    Sub Main()
        Dim root As XElement = XElement.Load("DataInNamespace.xml")
        Dim prices As IEnumerable(Of Decimal) = _
            From el In root.<Data> _
            Let price = Convert.ToDecimal(el.<Price>.Value) _
            Order By (price) _
            Select price
        For Each el As Decimal In prices
            Console.WriteLine(el)
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
0.99
4.95
6.99
24.50
29.00
66.00
89.99
```

## <a name="see-also"></a>Confira também

- [Classificando dados (C#)](../../csharp/programming-guide/concepts/linq/sorting-data.md)
- [Classificando dados (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/sorting-data.md)
- [Consultas básicas (LINQ to XML) (Visual Basic)](./find-element-specific-attribute.md)
