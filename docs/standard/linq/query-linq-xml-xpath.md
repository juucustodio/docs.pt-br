---
title: Como consultar LINQ to XML usando XPath-LINQ to XML
description: Aprenda os métodos de extensão que permitem consultar uma árvore XML usando XPath.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: ee5af263-4ab1-45e5-b792-33a3221b426d
ms.openlocfilehash: 8189bcdd38f9242a5890837633bbec4e7f2fc601
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552077"
---
# <a name="how-to-query-linq-to-xml-using-xpath-linq-to-xml"></a>Como consultar LINQ to XML usando XPath (LINQ to XML)

Este artigo apresenta os métodos de extensão que permitem consultar uma árvore XML usando XPath. Para obter informações detalhadas sobre como usar esses métodos de extensão, consulte <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>.

> [!NOTE]
> A menos que você tenha um motivo muito específico para consultar usando XPath, como o uso extensivo de código herdado, não é recomendável usar o XPath com o LINQ to XML. As consultas XPath não serão executadas, bem como consultas LINQ to XML.

## <a name="example"></a>Exemplo

O exemplo a seguir cria uma árvore XML pequena e usa <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> para selecionar um conjunto de elementos.

```csharp
XElement root = new XElement("Root",
    new XElement("Child1", 1),
    new XElement("Child1", 2),
    new XElement("Child1", 3),
    new XElement("Child2", 4),
    new XElement("Child2", 5),
    new XElement("Child2", 6)
);
IEnumerable<XElement> list = root.XPathSelectElements("./Child2");
foreach (XElement el in list)
    Console.WriteLine(el);
```

```vb
Dim root As XElement = _
    <Root>
        <Child1>1</Child1>
        <Child1>2</Child1>
        <Child1>3</Child1>
        <Child2>4</Child2>
        <Child2>5</Child2>
        <Child2>6</Child2>
    </Root>

Dim list As IEnumerable(Of XElement) = root.XPathSelectElements("./Child2")
For Each el As XElement In list
    Console.WriteLine(el)
Next
```

Esse exemplo gera a saída a seguir:

```xml
<Child2>4</Child2>
<Child2>5</Child2>
<Child2>6</Child2>
```
