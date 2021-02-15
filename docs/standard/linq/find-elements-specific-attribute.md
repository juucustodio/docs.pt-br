---
title: Como localizar elementos com um atributo específico-LINQ to XML
description: 'Saiba como localizar todos os elementos que têm um atributo específico (independentemente do valor). Dois métodos são mostrados: um usa XPathEvaluate, o outro usa LINQ to XML consulta.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: daed00dd-923a-43be-8a90-eee406f6f574
ms.openlocfilehash: 2a747e7609e2b130249a7635d8448577d035f939
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90545645"
---
# <a name="how-to-find-elements-with-a-specific-attribute-linq-to-xml"></a>Como localizar elementos com um atributo específico (LINQ to XML)

Este artigo mostra como usar o <xref:System.Xml.XPath.Extensions.XPathEvaluate%2A> para localizar todos os elementos que têm um atributo específico (independentemente do valor) e como usar LINQ to XML consulta para fazer a mesma coisa.

## <a name="example-find-all-elements-that-have-the-select-attribute"></a>Exemplo: localizar todos os elementos que têm o `Select` atributo

O exemplo a seguir cria uma árvore XML e, em seguida, localiza os elementos que têm o `Select` atributo.

A expressão XPath é `./*[@Select]`.

```csharp
XElement doc = XElement.Parse(
@"<Root>
    <Child1>1</Child1>
    <Child2 Select='true'>2</Child2>
    <Child3>3</Child3>
    <Child4 Select='true'>4</Child4>
    <Child5>5</Child5>
</Root>");

// LINQ to XML query
IEnumerable<XElement> list1 =
    from el in doc.Elements()
    where el.Attribute("Select") != null
    select el;

// XPath expression
IEnumerable<XElement> list2 =
    ((IEnumerable)doc.XPathEvaluate("./*[@Select]")).Cast<XElement>();

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim doc As XElement = _
    <Root>
        <Child1>1</Child1>
        <Child2 Select='true'>2</Child2>
        <Child3>3</Child3>
        <Child4 Select='true'>4</Child4>
        <Child5>5</Child5>
    </Root>

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = _
    From el In doc.Elements() _
    Where el.@Select <> Nothing _
    Select el

' XPath expression
Dim list2 As IEnumerable(Of XElement) = DirectCast(doc.XPathEvaluate _
    ("./*[@Select]"), IEnumerable).Cast(Of XElement)()

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
<Child2 Select="true">2</Child2>
<Child4 Select="true">4</Child4>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](./comparison-xpath-linq-xml.md)
