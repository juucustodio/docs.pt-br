---
title: Visão geral da classe XDocument
description: A classe LINQ to XML XDocument contém as informações necessárias para um documento XML válido. Em muitos casos, você não precisa da funcionalidade de um objeto XDocument e pode usar um objeto XElement em vez disso.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 63305603-ab54-49fc-84e4-f76eecc59549
ms.openlocfilehash: c26b7ac42733aad24d831f4a0a181e0fd8275eaf
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551853"
---
# <a name="xdocument-class-overview"></a>Visão geral da classe XDocument

A <xref:System.Xml.Linq.XDocument> classe contém as informações necessárias para um documento XML válido, que inclui uma declaração XML, instruções de processamento e comentários.

Você só precisa criar <xref:System.Xml.Linq.XDocument> objetos se precisar da funcionalidade específica fornecida pela <xref:System.Xml.Linq.XDocument> classe. Em muitas circunstâncias, você pode trabalhar diretamente com <xref:System.Xml.Linq.XElement>. Trabalhar diretamente com <xref:System.Xml.Linq.XElement> é um modelo de programação mais simples.

<xref:System.Xml.Linq.XDocument> deriva de <xref:System.Xml.Linq.XContainer> , portanto, ele pode conter nós filho. Entretanto, os objetos <xref:System.Xml.Linq.XDocument> podem ter apenas um nó <xref:System.Xml.Linq.XElement> filho. Isso reflete o padrão XML de que pode haver apenas um elemento raiz em um documento XML.

## <a name="components-of-xdocument"></a>Componentes de XDocument

Um <xref:System.Xml.Linq.XDocument> pode conter os seguintes elementos:

- Um objeto <xref:System.Xml.Linq.XDeclaration>. <xref:System.Xml.Linq.XDeclaration> permite que você especifique as partes pertinentes de uma declaração XML: a versão XML, a codificação do documento e se o documento XML é autônomo.
- Um objeto <xref:System.Xml.Linq.XElement>. Esse objeto é o nó raiz do documento XML.
- Qualquer número de objetos <xref:System.Xml.Linq.XProcessingInstruction>. Uma instrução de processamento comunica informações a um aplicativo que processa o XML.
- Qualquer número de objetos <xref:System.Xml.Linq.XComment>. Os comentários serão irmãos do elemento raiz. O <xref:System.Xml.Linq.XComment> objeto não pode ser o primeiro argumento na lista, porque não é válido para um documento XML começar com um comentário.
- Um <xref:System.Xml.Linq.XDocumentType> para o DTD.

Quando você serializa um <xref:System.Xml.Linq.XDocument>, mesmo que `XDocument.Declaration` seja `null`, a saída terá uma declaração XML se o gravador tiver `Writer.Settings.OmitXmlDeclaration` definido como `false` (o padrão).

Por padrão, LINQ to XML define a versão como "1,0" e define a codificação como "UTF-8".

## <a name="use-xelement-without-xdocument"></a>Usar XElement sem XDocument

Como mencionado anteriormente, a <xref:System.Xml.Linq.XElement> classe é a classe principal na interface de programação de LINQ to XML. Em muitos casos, seu aplicativo não exigirá que você crie um documento. Usando a <xref:System.Xml.Linq.XElement> classe, você pode:

- Crie uma árvore XML.
- Adicione outras árvores XML a ela.
- Modifique a árvore XML.
- Salve-o.

## <a name="use-xdocument"></a>Usar XDocument

Para construir um <xref:System.Xml.Linq.XDocument>, use a construção funcional exatamente como você faz para criar objetos <xref:System.Xml.Linq.XElement>.

O exemplo a seguir cria um <xref:System.Xml.Linq.XDocument> objeto e seus objetos contidos associados.

```csharp
XDocument d = new XDocument(
    new XComment("This is a comment."),
    new XProcessingInstruction("xml-stylesheet",
        "href='mystyle.css' title='Compact' type='text/css'"),
    new XElement("Pubs",
        new XElement("Book",
            new XElement("Title", "Artifacts of Roman Civilization"),
            new XElement("Author", "Moreno, Jordao")
        ),
        new XElement("Book",
            new XElement("Title", "Midieval Tools and Implements"),
            new XElement("Author", "Gazit, Inbar")
        )
    ),
    new XComment("This is another comment.")
);
d.Declaration = new XDeclaration("1.0", "utf-8", "true");
Console.WriteLine(d);

d.Save("test.xml");
```

```vb
Dim doc As XDocument = <?xml version="1.0" encoding="utf-8"?>
                       <!--This is a comment.-->
                       <?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>
                       <Pubs>
                           <Book>
                               <Title>Artifacts of Roman Civilization</Title>
                               <Author>Moreno, Jordao</Author>
                           </Book>
                           <Book>
                               <Title>Midieval Tools and Implements</Title>
                               <Author>Gazit, Inbar</Author>
                           </Book>
                       </Pubs>
                       <!--This is another comment.-->
doc.Save("test.xml")
```

O exemplo produz essa saída no test.xml:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--This is a comment.-->
<?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>
<Pubs>
  <Book>
    <Title>Artifacts of Roman Civilization</Title>
    <Author>Moreno, Jordao</Author>
  </Book>
  <Book>
    <Title>Midieval Tools and Implements</Title>
    <Author>Gazit, Inbar</Author>
  </Book>
</Pubs>
<!--This is another comment.-->
```

## <a name="see-also"></a>Confira também

- [Visão geral de LINQ to XML](linq-xml-overview.md)
