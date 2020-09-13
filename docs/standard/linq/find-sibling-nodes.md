---
title: Como encontrar nós irmãos-LINQ to XML
description: 'Saiba como localizar todos os irmãos de um nó que têm um nome específico. Dois métodos são mostrados: um usa XPathSelectElements, o outro usa LINQ to XML consulta.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: e2c73d10-a8ca-4e11-b5aa-d055de285874
ms.openlocfilehash: 3c764cec818cf788282bb616cc123e9be8d62c08
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551929"
---
# <a name="how-to-find-sibling-nodes-linq-to-xml"></a>Como localizar nós irmãos (LINQ to XML)

Este artigo mostra como usar o <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> para localizar todos os irmãos de um nó que têm um nome específico e como usar LINQ to XML consulta para fazer a mesma coisa.

> [!NOTE]
> A coleção resultante incluirá o nó de contexto se ele também tiver o nome específico.

## <a name="example-find-an-element-named-book-and-all-sibling-elements-named-book"></a>Exemplo: localizar um elemento chamado `Book` e todos os elementos irmãos chamados `Book`

Este exemplo primeiro localiza um `Book` elemento no [arquivo XML de exemplo](sample-xml-file-books.md)de documento XML: livros e localiza todos os elementos irmãos chamados `Book` . A coleção resultante inclui o nó de contexto.

A expressão XPath é `../Book`

```csharp
XDocument books = XDocument.Load("Books.xml");

XElement book =
    books
    .Root
    .Elements("Book")
    .Skip(1)
    .First();

// LINQ to XML query
IEnumerable<XElement> list1 =
    book
    .Parent
    .Elements("Book");

// XPath expression
IEnumerable<XElement> list2 = book.XPathSelectElements("../Book");

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim books As XDocument = XDocument.Load("Books.xml")
Dim book As XElement = books.Root.<Book>.Skip(1).First()

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = book.Parent.<Book>

' XPath expression
Dim list2 As IEnumerable(Of XElement) = book.XPathSelectElements("../Book")

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
<Book id="bk101">
  <Author>Garghentini, Davide</Author>
  <Title>XML Developer's Guide</Title>
  <Genre>Computer</Genre>
  <Price>44.95</Price>
  <PublishDate>2000-10-01</PublishDate>
  <Description>An in-depth look at creating applications
      with XML.</Description>
</Book>
<Book id="bk102">
  <Author>Garcia, Debra</Author>
  <Title>Midnight Rain</Title>
  <Genre>Fantasy</Genre>
  <Price>5.95</Price>
  <PublishDate>2000-12-16</PublishDate>
  <Description>A former architect battles corporate zombies,
      an evil sorceress, and her own childhood to become queen
      of the world.</Description>
</Book>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
