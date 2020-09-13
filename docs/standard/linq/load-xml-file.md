---
title: Como carregar XML de um arquivo-LINQ to XML
description: Você pode usar o método XElement. Load em C# e Visual Basic para carregar um documento XML de um arquivo.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 3ed38487-8028-4209-9872-c8dce0ed4dfe
ms.openlocfilehash: 7ac77205eb1f7637982e8f40d31df0a422ecba22
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551969"
---
# <a name="how-to-load-xml-from-a-file-linq-to-xml"></a>Como carregar XML de um arquivo (LINQ to XML)

Este artigo mostra como carregar XML de um arquivo em C# e Visual Basic usando o <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType> método.

## <a name="example-load-xml-document-from-a-file"></a>Exemplo: carregar documento XML de um arquivo

O exemplo a seguir mostra como carregar um documento XML de um arquivo, fornecendo <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType> com o URI que faz referência ao arquivo. O exemplo carrega books.xml e gera a árvore XML para o console.

O conteúdo de books.xml é mostrado no [arquivo XML de exemplo: livros](sample-xml-file-books.md).

```csharp
XElement booksFromFile = XElement.Load(@"books.xml");
Console.WriteLine(booksFromFile);
```

```vb
Dim booksFromFile As XElement = XElement.Load("books.xml")
Console.WriteLine(booksFromFile)
```

Esse exemplo gera a saída a seguir:

```xml
<Catalog>
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
</Catalog>
```
