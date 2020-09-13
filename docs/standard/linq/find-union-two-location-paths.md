---
title: Como localizar uma União de dois caminhos de local-LINQ to XML
description: 'Saiba como localizar a União dos resultados de dois caminhos de local XPath. Dois métodos são mostrados: um usa XPathSelectElements, o outro usa o operador de consulta padrão Concat.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 069622d3-2b58-4919-8903-710a564c0788
ms.openlocfilehash: ba2a1eef73a586074c75a7fec84c912acb8b25e9
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551912"
---
# <a name="how-to-find-a-union-of-two-location-paths-linq-to-xml"></a>Como localizar uma União de dois caminhos de local (LINQ to XML)

Este artigo mostra como usar <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> o para localizar a União dos resultados de dois caminhos de local XPath e como usar o operador de <xref:System.Linq.Enumerable.Concat%2A> consulta padrão para fazer a mesma coisa.

## <a name="example-find-all-category-and-price-elements-and-concatenate-them"></a>Exemplo: localizar todos `Category` os `Price` elementos e e concatena-los

Este exemplo localiza todos os `Category` elementos e todos os `Price` elementos em um arquivo XML de exemplo de documento XML [: dados numéricos](sample-xml-file-numerical-data.md)e os concatena em uma única coleção. A expressão XPath é `//Category|//Price`.

> [!NOTE]
> A consulta LINQ to XML chama <xref:System.Xml.Linq.Extensions.InDocumentOrder%2A> para colocar os resultados em ordem de documento. Os resultados da expressão XPath também estão em ordem de documento.

```csharp
XDocument data = XDocument.Load("Data.xml");

// LINQ to XML query
IEnumerable<XElement> list1 =
    data
    .Descendants("Category")
    .Concat(
        data
        .Descendants("Price")
    )
    .InDocumentOrder();

// XPath expression
IEnumerable<XElement> list2 = data.XPathSelectElements("//Category|//Price");

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim data As XDocument = XDocument.Load("Data.xml")

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = _
    data...<Category>.Concat(data...<Price>).InDocumentOrder()

' XPath expression
Dim list2 As IEnumerable(Of XElement) = _
    data.XPathSelectElements("//Category|//Price")

If list1.Count() = list2.Count() And _
        list1.Intersect(list2).Count() = list1.Count() Then
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
<Category>A</Category>
<Price>24.50</Price>
<Category>B</Category>
<Price>89.99</Price>
<Category>A</Category>
<Price>4.95</Price>
<Category>A</Category>
<Price>66.00</Price>
<Category>B</Category>
<Price>.99</Price>
<Category>A</Category>
<Price>29.00</Price>
<Category>B</Category>
<Price>6.99</Price>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
