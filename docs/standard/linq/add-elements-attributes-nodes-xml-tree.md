---
title: Adicionar elementos, atributos e nós a uma árvore XML-LINQ to XML
description: Saiba como adicionar conteúdo (elementos, atributos, comentários, instruções de processamento, texto e CDATA) a uma árvore XML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: db911e4f-40aa-499a-9500-a9763bb6df56
ms.openlocfilehash: 272605982bb7f5e6569ff2aa0ceb990f9c3b2d42
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400840"
---
# <a name="add-elements-attributes-and-nodes-to-an-xml-tree-linq-to-xml"></a>Adicionar elementos, atributos e nós a uma árvore XML (LINQ to XML)

Você pode adicionar conteúdo (elementos, atributos, comentários, instruções de processamento, texto e CDATA) a uma árvore XML.

## <a name="methods-for-adding-content"></a>Métodos para adicionar conteúdo

Os seguintes métodos adicionam conteúdo filho a um <xref:System.Xml.Linq.XElement> ou a um <xref:System.Xml.Linq.XDocument>:

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XContainer.Add%2A>|Adiciona conteúdo ao final do conteúdo filho de <xref:System.Xml.Linq.XContainer>.|
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|Adiciona conteúdo ao início do conteúdo filho de <xref:System.Xml.Linq.XContainer>.|

Os seguintes métodos adicionam o conteúdo como nós irmãos de um <xref:System.Xml.Linq.XNode>. O nó mais comum ao qual você adiciona conteúdo irmão é <xref:System.Xml.Linq.XElement>, embora você possa adicionar conteúdo irmão válido a outros tipos de nós como <xref:System.Xml.Linq.XText> ou <xref:System.Xml.Linq.XComment>.

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|Adiciona conteúdo depois de <xref:System.Xml.Linq.XNode>.|
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|Adiciona conteúdo antes de <xref:System.Xml.Linq.XNode>.|

## <a name="example-create-two-xml-trees-and-modify-one-of-them"></a>Exemplo: criar duas árvores XML e modificar uma delas

O exemplo a seguir cria duas árvores XML e, em seguida, modifica uma delas.

```csharp
var srcTree = new XElement("Root",
    new XElement("Element1", 1),
    new XElement("Element2", 2),
    new XElement("Element3", 3),
    new XElement("Element4", 4),
    new XElement("Element5", 5)
);
var xmlTree = new XElement("Root",
    new XElement("Child1", 1),
    new XElement("Child2", 2),
    new XElement("Child3", 3),
    new XElement("Child4", 4),
    new XElement("Child5", 5)
);
xmlTree.Add(new XElement("NewChild", "new content"));
xmlTree.Add(
    from el in srcTree.Elements()
    where (int)el > 3
    select el
);
// Even though Child9 doesn't exist in srcTree, the following statement won't
// throw an exception, and nothing will be added to xmlTree.
xmlTree.Add(srcTree.Element("Child9"));
Console.WriteLine(xmlTree);
```

```vb
Dim srcTree As XElement =
    <Root>
        <Element1>1</Element1>
        <Element2>2</Element2>
        <Element3>3</Element3>
        <Element4>4</Element4>
        <Element5>5</Element5>
    </Root>
Dim xmlTree As XElement =
    <Root>
        <Child1>1</Child1>
        <Child2>2</Child2>
        <Child3>3</Child3>
        <Child4>4</Child4>
        <Child5>5</Child5>
    </Root>

xmlTree.Add(<NewChild>new content</NewChild>)
xmlTree.Add(
    From el In srcTree.Elements()
    Where CInt(el) > 3
    Select el)

' Even though Child9 doesn't exist in srcTree, the following statement
' won't throw an exception, and nothing will be added to xmlTree.
xmlTree.Add(srcTree.Element("Child9"))
Console.WriteLine(xmlTree)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Child1>1</Child1>
  <Child2>2</Child2>
  <Child3>3</Child3>
  <Child4>4</Child4>
  <Child5>5</Child5>
  <NewChild>new content</NewChild>
  <Element4>4</Element4>
  <Element5>5</Element5>
</Root>
```
