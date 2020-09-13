---
title: Como escrever consultas em XML em namespaces-LINQ to XML
description: Para gravar uma consulta em XML que está em um namespace, use objetos XName que têm o namespace correto. Saiba como fazer isso em C# e Visual Basic e como criar consultas.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 7c54df81-15e4-4091-8c81-a87637029130
ms.openlocfilehash: 7d2c765c30409b019bf4723b9161c577e2074c04
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551888"
---
# <a name="how-to-write-queries-on-xml-in-namespaces-linq-to-xml"></a>Como escrever consultas em XML em namespaces (LINQ to XML)

Para gravar uma consulta em XML que está em um namespace, você deve usar <xref:System.Xml.Linq.XName> objetos que têm o namespace correto.

Para C#, a abordagem mais comum é inicializar um <xref:System.Xml.Linq.XNamespace> usando uma cadeia de caracteres que contém o URI, em seguida, usar a sobrecarga de operador de adição para combinar o namespace com o nome local.

Por Visual Basic, a abordagem mais comum é definir um namespace global e, em seguida, usar literais XML e propriedades XML que usam o namespace global. Você pode definir um namespace global padrão nesse caso, no qual os elementos nos literais XML estarão no namespace por padrão. Como alternativa, você pode definir um namespace global com um prefixo e, em seguida, usar o prefixo conforme necessário nos literais XML e nas propriedades XML. Como ocorre com outros formatos de XML, os atributos estão sempre em nenhum namespace por padrão.

O primeiro exemplo neste artigo mostra como criar uma árvore XML em um namespace padrão. O segundo mostra como criar uma árvore XML em um namespace com um prefixo.

## <a name="example-create-a-tree-in-a-default-namespace-and-retrieve-elements"></a>Exemplo: criar uma árvore em um namespace padrão e recuperar elementos

O exemplo a seguir cria uma árvore XML que está em um namespace padrão e, em seguida, recupera uma coleção de elementos.

```csharp
XNamespace aw = "http://www.adventure-works.com";
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
    from el in root.Elements(aw + "Child")
    select el;
foreach (XElement el in c1)
    Console.WriteLine((int)el);
```

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <Root>
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
        For Each el As XElement In c1
            Console.WriteLine(el.Value)
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
1
2
3
```

## <a name="example-create-a-tree-in-a-namespace-with-a-prefix-and-retrieve-elements"></a>Exemplo: criar uma árvore em um namespace com um prefixo e recuperar elementos

No C#, você escreve consultas da mesma maneira, independentemente de estar escrevendo consultas em uma árvore XML que usa um namespace com um prefixo ou em uma árvore XML com um namespace padrão.

O exemplo a seguir cria uma árvore XML que está em um namespace com um prefixo e, em seguida, recupera uma coleção de elementos.

```csharp
XNamespace aw = "http://www.adventure-works.com";
XElement root = XElement.Parse(
@"<aw:Root xmlns:aw='http://www.adventure-works.com'>
    <aw:Child>1</aw:Child>
    <aw:Child>2</aw:Child>
    <aw:Child>3</aw:Child>
    <aw:AnotherChild>4</aw:AnotherChild>
    <aw:AnotherChild>5</aw:AnotherChild>
    <aw:AnotherChild>6</aw:AnotherChild>
</aw:Root>");
IEnumerable<XElement> c1 =
    from el in root.Elements(aw + "Child")
    select el;
foreach (XElement el in c1)
    Console.WriteLine((int)el);
```

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <aw:Root>
                <aw:Child>1</aw:Child>
                <aw:Child>2</aw:Child>
                <aw:Child>3</aw:Child>
                <aw:AnotherChild>4</aw:AnotherChild>
                <aw:AnotherChild>5</aw:AnotherChild>
                <aw:AnotherChild>6</aw:AnotherChild>
            </aw:Root>
        Dim c1 As IEnumerable(Of XElement) = _
            From el In root.<aw:Child> _
            Select el
        For Each el As XElement In c1
            Console.WriteLine(CInt(el))
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
1
2
3
```

## <a name="see-also"></a>Confira também

- [Visão geral dos namespaces](namespaces-overview.md)
