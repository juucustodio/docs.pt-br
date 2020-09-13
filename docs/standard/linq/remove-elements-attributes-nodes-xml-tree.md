---
title: Remover elementos, atributos e nós de uma árvore XML-LINQ to XML
description: Saiba como remover elementos, atributos e outros tipos de nós de uma árvore XML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 07dd06d6-1117-4077-bf98-9120cf51176e
ms.openlocfilehash: 1a7c10892ccf1baaab7dde700266a134abe727de
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552071"
---
# <a name="remove-elements-attributes-and-nodes-from-an-xml-tree-linq-to-xml"></a>Remover elementos, atributos e nós de uma árvore XML (LINQ to XML)

Você pode modificar uma árvore XML, remover elementos, atributos e outros tipos de nós.

Remover um único elemento ou um único atributo de um documento XML é simples. No entanto, ao remover coleções de elementos ou atributos, você deve primeiro materializar uma coleção em uma lista e depois excluir os elementos ou os atributos da lista. A melhor abordagem é usar o <xref:System.Xml.Linq.Extensions.Remove%2A> método de extensão para fazer isso.

O principal motivo para usar essa abordagem é que a maioria das coleções recuperadas de uma árvore XML são geradas usando a execução adiada. Se você não os materializar primeiro em uma lista ou se não usar os métodos de extensão, poderá encontrar uma determinada classe de bugs. Para obter mais informações, consulte [bugs de código declarativo/imperativo misto](mixed-declarative-imperative-code-bugs.md).

Os métodos a seguir removem nós e atributos de uma árvore XML.

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Linq.XAttribute.Remove%2A?displayProperty=nameWithType>|Remova um <xref:System.Xml.Linq.XAttribute> de seu pai.|
|<xref:System.Xml.Linq.XContainer.RemoveNodes%2A?displayProperty=nameWithType>|Remova os nós filho de um <xref:System.Xml.Linq.XContainer> .|
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=nameWithType>|Remova o conteúdo e os atributos de um <xref:System.Xml.Linq.XElement> .|
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=nameWithType>|Remova os atributos de um <xref:System.Xml.Linq.XElement> .|
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=nameWithType>|Remova o atributo se você passar o valor `null` .|
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=nameWithType>|Remova o elemento filho se você passar o valor `null` .|
|<xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=nameWithType>|Remova um <xref:System.Xml.Linq.XNode> de seu pai.|
|<xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=nameWithType>|Remova todos os atributos ou elementos na coleção de origem do elemento pai.|

## <a name="example-remove-a-single-element-and-remove-a-collection-of-elements-in-two-ways"></a>Exemplo: remover um único elemento e remover uma coleção de elementos de duas maneiras

Este exemplo demonstra três abordagens para remover elementos. Primeiro, ele remove um único elemento. Em segundo lugar, ele recupera uma coleção de elementos, materializa-os usando o <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> operador e, em seguida, remove a coleção. Por último, recupera uma coleção de elementos e remove-a usando o método de extensão <xref:System.Xml.Linq.Extensions.Remove%2A>.

Para obter mais informações sobre o <xref:System.Linq.Enumerable.ToList%2A> operador, consulte [convertendo tipos de dados (C#)](../../csharp/programming-guide/concepts/linq/converting-data-types.md) e [convertendo tipos de dados (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/converting-data-types.md).

```csharp
XElement root = XElement.Parse(@"<Root>
    <Child1>
        <GrandChild1/>
        <GrandChild2/>
        <GrandChild3/>
    </Child1>
    <Child2>
        <GrandChild4/>
        <GrandChild5/>
        <GrandChild6/>
    </Child2>
    <Child3>
        <GrandChild7/>
        <GrandChild8/>
        <GrandChild9/>
    </Child3>
</Root>");
root.Element("Child1").Element("GrandChild1").Remove();
root.Element("Child2").Elements().ToList().Remove();
root.Element("Child3").Elements().Remove();
Console.WriteLine(root);
```

```vb
Dim root As XElement = _
    <Root>
        <Child1>
            <GrandChild1/>
            <GrandChild2/>
            <GrandChild3/>
        </Child1>
        <Child2>
            <GrandChild4/>
            <GrandChild5/>
            <GrandChild6/>
        </Child2>
        <Child3>
            <GrandChild7/>
            <GrandChild8/>
            <GrandChild9/>
        </Child3>
    </Root>
root.<Child1>.<GrandChild1>.Remove()
root.<Child2>.Elements().ToList().Remove()
root.<Child3>.Elements().Remove()
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Child1>
    <GrandChild2 />
    <GrandChild3 />
  </Child1>
  <Child2 />
  <Child3 />
</Root>
```

O primeiro elemento neto foi removido de `Child1` e todos os elementos netos foram removidos de `Child2` e de `Child3` .
