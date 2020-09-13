---
title: Como controlar prefixos de namespace-LINQ to XML
description: Você pode controlar prefixos de namespace ao serializar uma árvore XML em C# e Visual Basic. Para fazer isso, insira atributos que declaram namespaces.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 64de5186-b81a-4ddd-8327-8693df59a01b
ms.openlocfilehash: 07efc23c11cd0dc0d281968911cf24d6ecbc76a2
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551885"
---
# <a name="how-to-control-namespace-prefixes-linq-to-xml"></a>Como controlar prefixos de namespace (LINQ to XML)

Este artigo descreve como controlar prefixos de namespace ao serializar uma árvore XML em C# e Visual Basic.

Em muitas situações, não é necessário controlar prefixos de namespace. No entanto, algumas ferramentas de programação XML exigem isso. Por exemplo, você pode estar manipulando uma folha de estilos XSLT ou um documento XAML que contém expressões XPath inseridas que se referem a prefixos de namespaces específicos. Nesse caso, é importante que o documento seja serializado com esses prefixos. Esse é um motivo comum para controlar prefixos de namespace.

Outro motivo é que você deseja que os usuários editem o documento XML manualmente e queira criar prefixos de namespace que são convenientes para o usuário digitar. Por exemplo, você pode estar gerando um documento XSD. As convenções de esquemas sugerem que você use `xs` ou `xsd` como o prefixo do namespace do esquema.

Para controlar prefixos de namespace, você insere os atributos que declaram os namespaces. Se você declarar os namespaces com prefixos específicos, LINQ to XML tentará respeitar os prefixos de namespace ao serializar.

Para criar um atributo que declare um namespace com um prefixo, você cria um atributo onde o namespace do nome do atributo é <xref:System.Xml.Linq.XNamespace.Xmlns%2A>, e o nome do atributo é o prefixo do namespace. O valor do atributo é o URI do namespace.

## <a name="example-create-two-namespaces-that-have-prefixes"></a>Exemplo: criar dois namespaces que têm prefixos

Esse exemplo declara dois namespaces. Ele especifica o prefixo `aw` para o `http://www.adventure-works.com` namespace e o prefixo `fc` para o `www.fourthcoffee.com` namespace.

```csharp
XNamespace aw = "http://www.adventure-works.com";
XNamespace fc = "www.fourthcoffee.com";
XElement root = new XElement(aw + "Root",
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),
    new XAttribute(XNamespace.Xmlns + "fc", "www.fourthcoffee.com"),
    new XElement(fc + "Child",
        new XElement(aw + "DifferentChild", "other content")
    ),
    new XElement(aw + "Child2", "c2 content"),
    new XElement(fc + "Child3", "c3 content")
);
Console.WriteLine(root);
```

```vb
Imports <xmlns:aw="http://www.adventure-works.com">
Imports <xmlns:fc="www.fourthcoffee.com">

Module Module1

    Sub Main()
        Dim root As XElement = _
            <aw:Root>
                <fc:Child>
                    <aw:DifferentChild>other content</aw:DifferentChild>
                </fc:Child>
                <aw:Child2>c2 content</aw:Child2>
                <fc:Child3>c3 content</fc:Child3>
            </aw:Root>
        Console.WriteLine(root)
    End Sub

This example produces the following output:

```xml
<aw:Root xmlns:aw="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">
  <fc:Child>
    <aw:DifferentChild>other content</aw:DifferentChild>
  </fc:Child>
  <aw:Child2>c2 content</aw:Child2>
  <fc:Child3>c3 content</fc:Child3>
</aw:Root>
```

## <a name="see-also"></a>Confira também

- [Visão geral dos namespaces](namespaces-overview.md)
