---
title: Como localizar um atributo do LINQ to XML pai
description: 'Saiba como navegar para um elemento e localizar um atributo de seu pai. Dois métodos são mostrados: um usa XPathEvaluate, o outro usa LINQ to XML consulta.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: dbef9d89-a5c4-431f-80cc-7a2ebf323f86
ms.openlocfilehash: 811766ecfdf2f080f29f21ae08981483f75a7e44
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552334"
---
# <a name="how-to-find-an-attribute-of-the-parent-linq-to-xml"></a>Como localizar um atributo do pai (LINQ to XML)

Este artigo mostra como usar <xref:System.Xml.XPath.Extensions.XPathEvaluate%2A> o para localizar um atributo de um elemento pai e como usar LINQ to XML consulta para fazer a mesma coisa.

## <a name="example-find-the-author-element-and-then-find-the-id-attribute-of-its-parent"></a>Exemplo: Localize o `Author` elemento e, em seguida, localize o `id` atributo de seu pai

Este exemplo primeiro localiza um `Author` elemento no [arquivo XML de exemplo](sample-xml-file-books.md)de documento XML: livros e, em seguida, localiza o `id` atributo de seu elemento pai.

A expressão XPath é `../@id`.

```csharp
XDocument books = XDocument.Load("Books.xml");

XElement author =
    books
    .Root
    .Element("Book")
    .Element("Author");

// LINQ to XML query
XAttribute att1 =
    author
    .Parent
    .Attribute("id");

// XPath expression
XAttribute att2 = ((IEnumerable)author.XPathEvaluate("../@id")).Cast<XAttribute>().First();

if (att1 == att2)
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
Console.WriteLine(att1);
```

```vb
Dim books As XDocument = XDocument.Load("Books.xml")
Dim author As XElement = books.Root.<Book>.<Author>.FirstOrDefault()

' LINQ to XML query
Dim att1 As XAttribute = author.Parent.Attribute("id")

' XPath expression
Dim att2 As XAttribute = DirectCast(author.XPathEvaluate("../@id"),  _
    IEnumerable).Cast(Of XAttribute)().First()

If att1 Is att2 Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
Console.WriteLine(att1)
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
id="bk101"
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
