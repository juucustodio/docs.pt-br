---
title: Como localizar atributos de irmãos com um nome específico-LINQ to XML
description: 'Saiba como localizar todos os atributos que têm um nome específico e que também pertencem a um irmão do nó de contexto. Dois métodos são mostrados: um usa XPathEvaluate, o outro usa LINQ to XML consulta.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: c3133d64-523f-422d-8838-73d36b945ca0
ms.openlocfilehash: ca332f013fe8aea90b6203f5b602ab219362f5d3
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552333"
---
# <a name="how-to-find-attributes-of-siblings-with-a-specific-name-linq-to-xml"></a>Como localizar atributos de irmãos com um nome específico (LINQ to XML)

Este artigo mostra como usar o <xref:System.Xml.XPath.Extensions.XPathEvaluate%2A> para localizar cada atributo que tem um nome específico e que também pertence a um irmão do nó de contexto. O artigo também mostra como usar LINQ to XML consulta para fazer a mesma coisa.

## <a name="example-find-all-sibling-elements-named-book-and-then-find-all-attributes-named-id"></a>Exemplo: localizar todos os elementos irmãos chamados `Book` e, em seguida, localizar todos os atributos chamados `id`

Este exemplo localiza um `Book` elemento no [arquivo XML de exemplo](sample-xml-file-books.md)de documento XML: livros. Em seguida, ele localiza todos os elementos irmãos chamados `Book` e todos os atributos nomeados `id` desses elementos. O resultado é uma coleção de atributos.

A expressão XPath é `../Book/@id`.

```csharp
XDocument books = XDocument.Load("Books.xml");

XElement book =
    books
    .Root
    .Element("Book");

// LINQ to XML query
IEnumerable<XAttribute> list1 =
    from el in book.Parent.Elements("Book")
    select el.Attribute("id");

// XPath expression
IEnumerable<XAttribute> list2 =
  ((IEnumerable)book.XPathEvaluate("../Book/@id")).Cast<XAttribute>();

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XAttribute el in list1)
    Console.WriteLine(el);
```

```vb
Dim books as XDocument = XDocument.Load("Books.xml")
Dim book As XElement = books.Root.<Book>(0)

' LINQ to XML query
Dim list1 As IEnumerable(Of XAttribute) = _
    From el In book.Parent.<Book> _
    Select el.Attribute("id")

' XPath expression
Dim list2 As IEnumerable(Of XAttribute) = DirectCast(book. _
    XPathEvaluate("../Book/@id"), IEnumerable).Cast(Of XAttribute)()

If list1.Count() = list2.Count() And _
        (list1.Intersect(list2)).Count() = list1.Count() Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If

For Each el As XAttribute In list1
    Console.WriteLine(el)
Next
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
id="bk101"
id="bk102"
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
