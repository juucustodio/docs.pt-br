---
title: Como localizar o LINQ to XML irmão precedentes imediatos
description: 'Saiba como localizar o irmão que precede imediatamente um nó. Dois métodos são mostrados: um usa XPathEvaluate, o outro usa LINQ to XML consulta.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 74c06201-0b1b-4b5e-b3ac-0092980614e6
ms.openlocfilehash: 9be39c20a99920482899efa934003957ffc696b7
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90545611"
---
# <a name="how-to-find-the-immediate-preceding-sibling-linq-to-xml"></a>Como localizar o irmão precedentes imediatos (LINQ to XML)

Este artigo mostra como usar <xref:System.Xml.XPath.Extensions.XPathEvaluate%2A> o para localizar o irmão que precede imediatamente um nó e como usar LINQ to XML consulta para fazer a mesma coisa. Devido à diferença na semântica de predicados de posição para os eixos irmãos precedentes em XPath em oposição a LINQ to XML, essa é uma das comparações mais interessantes.

## <a name="example-find-the-next-to-last-element"></a>Exemplo: encontrar o próximo ao último elemento

Neste exemplo, a consulta LINQ to XML usa o <xref:System.Linq.Enumerable.Last%2A> operador para localizar o último nó na coleção retornada por <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A> . Por outro lado, a expressão XPath usa um predicado com um valor de 1 para localizar o elemento imediatamente anterior.

```csharp
XElement root = XElement.Parse(
    @"<Root>
    <Child1/>
    <Child2/>
    <Child3/>
    <Child4/>
</Root>");
XElement child4 = root.Element("Child4");

// LINQ to XML query
XElement el1 =
    child4
    .ElementsBeforeSelf()
    .Last();

// XPath expression
XElement el2 =
    ((IEnumerable)child4
                 .XPathEvaluate("preceding-sibling::*[1]"))
                 .Cast<XElement>()
                 .First();

if (el1 == el2)
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
Console.WriteLine(el1);
```

```vb
Dim root As XElement = _
    <Root>
        <Child1/>
        <Child2/>
        <Child3/>
        <Child4/>
    </Root>
Dim child4 As XElement = root.Element("Child4")

' LINQ to XML query
Dim el1 As XElement = child4.ElementsBeforeSelf().Last()

' XPath expression
Dim el2 As XElement = _
    DirectCast(child4.XPathEvaluate("preceding-sibling::*[1]"),  _
    IEnumerable).Cast(Of XElement)().First()

If el1 Is el2 Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
Console.WriteLine(el1)
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
<Child3 />
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](./comparison-xpath-linq-xml.md)
