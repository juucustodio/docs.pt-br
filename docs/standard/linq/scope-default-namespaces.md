---
title: Escopo de namespaces padrão-LINQ to XML
description: Os namespaces padrão, conforme representado na árvore XML, não estão no escopo de consultas. Aqui estão as maneiras adequadas e inadequadas de consultá-las.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: fe826236-830f-457a-9027-7ad62c909fae
ms.openlocfilehash: 105309a70e5fbf48c4e595d4064b11fe0378f81e
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552323"
---
# <a name="scope-of-default-namespaces-linq-to-xml"></a>Escopo de namespaces padrão (LINQ to XML)

Os namespaces padrão, conforme representado na árvore XML, não estão no escopo de consultas. Se você tiver um XML que esteja em um namespace padrão, deverá combinar um namespace com o nome local para fazer com que um nome qualificado seja usado na consulta.

Um erro comum na consulta de uma árvore XML que tem um namespace padrão é gravar a consulta como se o XML estivesse em um namespace. O primeiro exemplo mostra uma consulta imprópria típica de um namespace padrão. O segundo mostra uma consulta apropriada.

## <a name="example-improper-query-of-xml-in-a-namespace"></a>Exemplo: consulta inadequada de XML em um namespace

Este exemplo mostra a criação de XML em um namespace e uma consulta inadequada que retorna um conjunto de resultados vazio.

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

Esse exemplo gera a saída a seguir:

```output
Result set follows:
End of result set
```

## <a name="example--proper-query-of-xml-in-a-namespace"></a>Exemplo: consulta apropriada de XML em um namespace

Este exemplo mostra a criação de XML em um namespace e uma consulta apropriada.

No C#, a abordagem correta é declarar e inicializar um <xref:System.Xml.Linq.XNamespace> objeto e usá-lo ao especificar <xref:System.Xml.Linq.XName> objetos. Nesse caso, o argumento para o método de <xref:System.Xml.Linq.XContainer.Elements%2A> é um objeto de <xref:System.Xml.Linq.XName> .

A abordagem correta para usar o Visual Basic é declarar e inicializar um namespace global padrão. Isso coloca todas as propriedades XML no namespace padrão.

Eis o código:

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
            Console.WriteLine(el.Value)
        Next
        Console.WriteLine("End of result set")
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
Result set follows:
1
2
3
End of result set
```

## <a name="see-also"></a>Confira também

- [Visão geral dos namespaces](namespaces-overview.md)
