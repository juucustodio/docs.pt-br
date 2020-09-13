---
title: Programando com nós-LINQ to XML
description: Saiba como codificar no nível de nó de uma árvore XML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: c38df0f2-c805-431a-93ff-9103a4284c2f
ms.openlocfilehash: 8f9d5c8656a06a9b40a3833aaf7e190b9ba3f0a6
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551965"
---
# <a name="programming-with-nodes-linq-to-xml"></a>Programando com nós (LINQ to XML)

LINQ to XML desenvolvedores que precisam escrever programas como um editor de XML, um sistema de transformação ou um gravador de relatório muitas vezes precisam de um código que funcione em um nível mais detalhado de granularidade do que elementos e atributos. Geralmente, eles precisam trabalhar no nível do nó, manipular nós de texto, instruções de processamento e comentários de processamento. Este artigo fornece informações sobre programação no nível do nó.

## <a name="example-the-parent-property-values-of-the-child-nodes-of-xdocument-are-set-to-null"></a>Exemplo: os `Parent` valores de propriedade dos nós filho de XDocument estão definidos como `null`

A propriedade de <xref:System.Xml.Linq.XObject.Parent%2A> contém <xref:System.Xml.Linq.XElement>pai, não o nó pai. Os nós filho de <xref:System.Xml.Linq.XDocument> não têm nenhum <xref:System.Xml.Linq.XElement>pai. Seu pai é o documento, portanto, a <xref:System.Xml.Linq.XObject.Parent%2A> propriedade para esses nós é definida como `null` .

O exemplo a seguir demonstra este:

```csharp
XDocument doc = XDocument.Parse(@"<!-- a comment --><Root/>");
Console.WriteLine(doc.Nodes().OfType<XComment>().First().Parent == null);
Console.WriteLine(doc.Root.Parent == null);
```

```vb
Dim doc As XDocument = XDocument.Parse("<!-- a comment --><Root/>")
Console.WriteLine(doc.Nodes().OfType(Of XComment).First().Parent Is Nothing)
Console.WriteLine(doc.Root.Parent Is Nothing)
```

Esse exemplo gera a saída a seguir:

```output
True
True
```

## <a name="example-adding-text-may-or-may-not-create-a-new-text-node"></a>Exemplo: adicionar texto pode ou não criar um novo nó de texto

Em um número XML que programa modelos, nós adjacentes de texto sempre são mesclados. Isso é às vezes chamado normalização de nós de texto. LINQ to XML não normaliza os nós de texto. Se você adicionar dois nós de texto ao mesmo elemento, resultará a nós adjacentes de texto. No entanto, se você adicionar conteúdo especificado como uma cadeia de caracteres em vez de como um <xref:System.Xml.Linq.XText> nó, LINQ to XML poderá mesclar a cadeia de caracteres com um nó de texto adjacente. O exemplo a seguir demonstra isso.

```csharp
XElement xmlTree = new XElement("Root", "Content");

Console.WriteLine(xmlTree.Nodes().OfType<XText>().Count());

// this doesn't add a new text node
xmlTree.Add("new content");
Console.WriteLine(xmlTree.Nodes().OfType<XText>().Count());

// this does add a new, adjacent text node
xmlTree.Add(new XText("more text"));
Console.WriteLine(xmlTree.Nodes().OfType<XText>().Count());
```

```vb
Dim xmlTree As XElement = <Root>Content</Root>
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())

' This doesn't add a new text node.
xmlTree.Add("new content")
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())

'// This does add a new, adjacent text node.
xmlTree.Add(New XText("more text"))
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())
```

 Esse exemplo gera a saída a seguir:

```output
1
1
2
```

## <a name="example-setting-a-text-node-value-to-the-empty-string-doesnt-delete-the-node"></a>Exemplo: definir um valor de nó de texto para a cadeia de caracteres vazia não exclui o nó

Em algum XML que programa modelos, os nós de texto são garantidos para não conter a cadeia de caracteres vazia. O raciocínio é que um nó de texto não tem impacto na serialização XML. No entanto, pelo mesmo motivo que os nós de texto adjacentes são possíveis, se você remover o texto de um nó de texto definindo seu valor para a cadeia de caracteres vazia, o nó de texto em si não será excluído.

```csharp
XElement xmlTree = new XElement("Root", "Content");
XText textNode = xmlTree.Nodes().OfType<XText>().First();

// the following line doesn't cause the removal of the text node.
textNode.Value = "";

XText textNode2 = xmlTree.Nodes().OfType<XText>().First();
Console.WriteLine(">>{0}<<", textNode2);
```

```vb
Dim xmlTree As XElement = <Root>Content</Root>
Dim textNode As XText = xmlTree.Nodes().OfType(Of XText)().First()

' The following line doesn't cause the removal of the text node.
textNode.Value = ""

Dim textNode2 As XText = xmlTree.Nodes().OfType(Of XText)().First()
Console.WriteLine(">>{0}<<", textNode2)
```

Esse exemplo gera a saída a seguir:

```output
>><<
```

## <a name="example-an-element-with-one-empty-text-node-is-serialized-differently-from-one-with-no-text-node"></a>Exemplo: um elemento com um nó de texto vazio é serializado de forma diferente de um sem nó de texto

Se um elemento contiver apenas um nó de texto filho vazio, ele será serializado com a sintaxe de marca longa: `<Child></Child>` . Se um elemento não contiver nenhum nó filho, ele será serializado com a sintaxe de marca curta: `<Child />` .

```csharp
XElement child1 = new XElement("Child1",
    new XText("")
);
XElement child2 = new XElement("Child2");
Console.WriteLine(child1);
Console.WriteLine(child2);
```

```vb
Dim child1 As XElement = New XElement("Child1", _
    New XText("") _
)
Dim child2 As XElement = New XElement("Child2")
Console.WriteLine(child1)
Console.WriteLine(child2)
```

Esse exemplo gera a saída a seguir:

```xml
<Child1></Child1>
<Child2 />
```

## <a name="example-namespaces-are-attributes-in-the-linq-to-xml-tree"></a>Exemplo: namespaces são atributos na árvore de LINQ to XML

Embora as declarações de namespace tenham sintaxe idêntica aos atributos, em algumas interfaces de programação, como XSLT e XPath, as declarações de namespace não são consideradas atributos. No entanto, no LINQ to XML, os namespaces são armazenados como <xref:System.Xml.Linq.XAttribute> objetos na árvore XML. Se você iterar pelos atributos de um elemento que contém uma declaração de namespace, a declaração de namespace será um dos itens na coleção retornada. A propriedade de <xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A> indica se um atributo é uma declaração de namespace.

```csharp
XElement root = XElement.Parse(
@"<Root
    xmlns='http://www.adventure-works.com'
    xmlns:fc='www.fourthcoffee.com'
    AnAttribute='abc'/>");
foreach (XAttribute att in root.Attributes())
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, att.IsNamespaceDeclaration);
```

```vb
Dim root As XElement = _
<Root
    xmlns='http://www.adventure-works.com'
    xmlns:fc='www.fourthcoffee.com'
    AnAttribute='abc'/>
For Each att As XAttribute In root.Attributes()
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, _
                      att.IsNamespaceDeclaration)
Next
```

Esse exemplo gera a saída a seguir:

```output
xmlns="http://www.adventure-works.com"  IsNamespaceDeclaration:True
xmlns:fc="www.fourthcoffee.com"  IsNamespaceDeclaration:True
AnAttribute="abc"  IsNamespaceDeclaration:False
```

## <a name="example-xpath-axis-methods-dont-return-the-child-text-nodes-of-xdocument"></a>Exemplo: os métodos do eixo XPath não retornam os nós de texto filho de XDocument

LINQ to XML permite nós de texto filho de um <xref:System.Xml.Linq.XDocument> , desde que os nós de texto contenham apenas espaços em branco. No entanto, o modelo de objeto XPath não inclui o espaço em branco como nós filho de um documento, portanto, quando você itera pelos filhos de um <xref:System.Xml.Linq.XDocument> usando o <xref:System.Xml.Linq.XContainer.Nodes%2A> eixo, nós de texto de espaço em branco serão retornados. No entanto, quando você itera através dos filhos de um <xref:System.Xml.Linq.XDocument> usando os métodos do eixo XPath, os nós de texto de espaço em branco não serão retornados.

```csharp
// Create a document with some white space child nodes of the document.
XDocument root = XDocument.Parse(
@"<?xml version='1.0' encoding='utf-8' standalone='yes'?>

<Root/>

<!--a comment-->
", LoadOptions.PreserveWhitespace);

// count the white space child nodes using LINQ to XML
Console.WriteLine(root.Nodes().OfType<XText>().Count());

// count the white space child nodes using XPathEvaluate
Console.WriteLine(((IEnumerable)root.XPathEvaluate("text()")).OfType<XText>().Count());
```

```vb
' Create a document with some white space child nodes of the document.
Dim root As XDocument = XDocument.Parse( _
"<?xml version='1.0' encoding='utf-8' standalone='yes'?>" & _
vbNewLine & "<Root/>" & vbNewLine & "<!--a comment-->" & vbNewLine, _
LoadOptions.PreserveWhitespace)

' Count the white space child nodes using LINQ to XML.
Console.WriteLine(root.Nodes().OfType(Of XText)().Count())

' Count the white space child nodes using XPathEvaluate.
Dim nodes As IEnumerable = CType(root.XPathEvaluate("text()"), IEnumerable)
Console.WriteLine(nodes.OfType(Of XText)().Count())
```

Esse exemplo gera a saída a seguir:

```output
3
0
```

### <a name="the-xml-declaration-node-of-an-xdocument-is-a-property-not-a-child-node"></a>O nó de declaração XML de um XDocument é uma propriedade, não um nó filho

Ao percorrer os nós filho de um <xref:System.Xml.Linq.XDocument> , você não verá o objeto de declaração XML. É uma propriedade do documento, não um nó filho dele.

```csharp
XDocument doc = new XDocument(
    new XDeclaration("1.0", "utf-8", "yes"),
    new XElement("Root")
);
doc.Save("Temp.xml");
Console.WriteLine(File.ReadAllText("Temp.xml"));

// this shows that there is only one child node of the document
Console.WriteLine(doc.Nodes().Count());
```

```vb
Dim doc As XDocument = _
<?xml version='1.0' encoding='utf-8' standalone='yes'?>
<Root/>

doc.Save("Temp.xml")
Console.WriteLine(File.ReadAllText("Temp.xml"))

' This shows that there is only one child node of the document.
Console.WriteLine(doc.Nodes().Count())
```

Esse exemplo gera a saída a seguir:

```output
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<Root />
1
```
