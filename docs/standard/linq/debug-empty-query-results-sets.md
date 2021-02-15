---
title: Como depurar conjuntos de resultados de consulta vazios-LINQ to XML
description: Quando você consulta uma árvore XML em um namespace padrão, evite o erro comum de consultar como se o XML não estivesse em um namespace.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b569f0dc-425e-45a6-acbf-770fb761c981
ms.openlocfilehash: 8fc6b1a80b183f8e2b0f80fc554a12c2657dcb55
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557138"
---
# <a name="how-to-debug-empty-query-results-sets-linq-to-xml"></a>Como depurar conjuntos de resultados de consulta vazios (LINQ to XML)

Um dos problemas mais comuns para o consulte árvores XML é que se a árvore tem um namespace XML padrão, o desenvolvedor escreve às vezes a consulta como se o XML não estar em um namespace.

O primeiro conjunto de exemplos neste artigo mostra uma maneira típica de o XML em um namespace padrão ser carregado e, em seguida, consultado de forma inadequada.

O segundo conjunto de exemplos a seguir mostra as correções necessárias para que você possa ver XML em um namespace.

Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

## <a name="example-an-improper-query-on-xml-in-a-namespace"></a>Exemplo: uma consulta inadequada em XML em um namespace

Este exemplo mostra como criar XML em um namespace, e uma consulta que retorna um conjunto de resultados vazia.

```csharp
XElement root = XElement.Parse(
@"<Root xmlns='http://www.adventure-works.com'>
    <Child>1</Child>
    <Child>2</Child>
    <Child>3</Child>
    <AnotherChild>4</AnotherChild>
    <AnotherChild>5</AnotherChild>
    <AnotherChild>6</AnotherChild>
</Root>");
IEnumerable<XElement> c1 =
    from el in root.Elements("Child")
    select el;
Console.WriteLine("Result set follows:");
foreach (XElement el in c1)
    Console.WriteLine((int)el);
Console.WriteLine("End of result set");
```

```vb
Dim root As XElement = _
    <Root xmlns='http://www.adventure-works.com'>
        <Child>1</Child>
        <Child>2</Child>
        <Child>3</Child>
        <AnotherChild>4</AnotherChild>
        <AnotherChild>5</AnotherChild>
        <AnotherChild>6</AnotherChild>
    </Root>
Dim c1 As IEnumerable(Of XElement) = _
        From el In root.<Child> _
        Select el
Console.WriteLine("Result set follows:")
For Each el As XElement In c1
    Console.WriteLine(el.Value)
Next
Console.WriteLine("End of result set")
```

O exemplo produz esse resultado:

```output
Result set follows:
End of result set
```

## <a name="example-a-proper-query-on-xml-in-a-namespace"></a>Exemplo: uma consulta apropriada em XML em um namespace

Este exemplo mostra a criação de XML em um namespace e uma consulta que é codificada corretamente.

A solução é declarar e inicializar um objeto de <xref:System.Xml.Linq.XNamespace> e usá-lo para especificar <xref:System.Xml.Linq.XName> objetos. Nesse caso, o argumento para o método de <xref:System.Xml.Linq.XContainer.Elements%2A> é um objeto de <xref:System.Xml.Linq.XName> .

```csharp
XElement root = XElement.Parse(
@"<Root xmlns='http://www.adventure-works.com'>
    <Child>1</Child>
    <Child>2</Child>
    <Child>3</Child>
    <AnotherChild>4</AnotherChild>
    <AnotherChild>5</AnotherChild>
    <AnotherChild>6</AnotherChild>
</Root>");
XNamespace aw = "http://www.adventure-works.com";
IEnumerable<XElement> c1 =
    from el in root.Elements(aw + "Child")
    select el;
Console.WriteLine("Result set follows:");
foreach (XElement el in c1)
    Console.WriteLine((int)el);
Console.WriteLine("End of result set");
```

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <Root xmlns='http://www.adventure-works.com'>
                <Child>1</Child>
                <Child>2</Child>
                <Child>3</Child>
                <AnotherChild>4</AnotherChild>
                <AnotherChild>5</AnotherChild>
                <AnotherChild>6</AnotherChild>
            </Root>
        Dim c1 As IEnumerable(Of XElement) = _
                From el In root.<Child> _
                Select el
        Console.WriteLine("Result set follows:")
        For Each el As XElement In c1
            Console.WriteLine(CInt(el))
        Next
        Console.WriteLine("End of result set")
    End Sub
End Module
```

O exemplo produz esse resultado:

```output
Result set follows:
1
2
3
End of result set
```

## <a name="see-also"></a>Confira também

- [Consultas básicas (LINQ to XML) (Visual Basic)](./find-element-specific-attribute.md)
