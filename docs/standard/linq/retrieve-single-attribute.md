---
title: Como recuperar um único atributo-LINQ to XML
description: Recupere um único atributo de um elemento, dado o nome do atributo.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 1b6b07b9-933f-47e9-874e-e790cab49dc5
ms.openlocfilehash: a8a56ec62275f2376d19d7fc9090414b74fc77ad
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552060"
---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml"></a>Como recuperar um único atributo (LINQ to XML)

Este artigo explica como recuperar um único atributo de um elemento, dado o nome do atributo. Isso é útil para gravar as expressões de consulta onde você deseja localizar um elemento que possui um atributo específico.

O método de <xref:System.Xml.Linq.XElement.Attribute%2A> da classe de <xref:System.Xml.Linq.XElement> retorna <xref:System.Xml.Linq.XAttribute> com o nome especificado.

## <a name="example-retrieve-attribute-values-given-the-element-and-attribute-names"></a>Exemplo: recuperar valores de atributo, considerando os nomes de elemento e atributo

O exemplo a seguir usa o <xref:System.Xml.Linq.XElement> método para criar um elemento chamado `PhoneNumbers` . Em seguida, ele localiza todos os elementos descendentes chamados `Phone` e, para cada um, usa o <xref:System.Xml.Linq.XElement.Attribute%2A> método para obter e gerar o valor do atributo chamado `type` :

```csharp
XElement cust = new XElement("PhoneNumbers",
    new XElement("Phone",
        new XAttribute("type", "home"),
        "555-555-5555"),
    new XElement("Phone",
        new XAttribute("type", "work"),
        "555-555-6666")
);
IEnumerable<XElement> elList =
    from el in cust.Descendants("Phone")
    select el;
foreach (XElement el in elList)
    Console.WriteLine((string)el.Attribute("type"));
```

```vb
Dim cust As XElement = <PhoneNumbers>
                           <Phone type="home">555-555-5555</Phone>
                           <Phone type="work">555-555-6666</Phone>
                       </PhoneNumbers>
Dim elList = From el In cust...<Phone>
For Each e As XElement In elList
    Console.WriteLine(e.@type)
Next
```

Esse exemplo gera a saída a seguir:

```output
home
work
```

## <a name="example-retrieve-an-attribute-value-with-a-cast"></a>Exemplo: recuperar um valor de atributo com uma conversão

Você pode recuperar o valor de um atributo, convertendo-o, assim como faz para com <xref:System.Xml.Linq.XElement> objetos. O exemplo a seguir demonstra este:

```csharp
XElement cust = new XElement("PhoneNumbers",
    new XElement("Phone",
        new XAttribute("type", "home"),
        "555-555-5555"),
    new XElement("Phone",
        new XAttribute("type", "work"),
        "555-555-6666")
);
IEnumerable<XElement> elList =
    from el in cust.Descendants("Phone")
    select el;
foreach (XElement el in elList)
    Console.WriteLine((string)el.Attribute("type"));
```

```vb
Dim cust As XElement = <PhoneNumbers>
                           <Phone type="home">555-555-5555</Phone>
                           <Phone type="work">555-555-6666</Phone>
                       </PhoneNumbers>
Dim elList As IEnumerable(Of XElement) = _
    From el In cust...<Phone> _
    Select el
For Each el As XElement In elList
    Console.WriteLine(el.@type)
Next
```

Esse exemplo gera a saída a seguir:

```output
home
work
```

LINQ to XML fornece operadores de conversão explícitos para a classe para,,,,,,,,, <xref:System.Xml.Linq.XAttribute> `string` `bool` ,, `bool?` `int` `int?` `uint` `uint?` `long` `long?` `ulong` `ulong?` `float` , `float?` ,, `double` , `double?` `decimal` `decimal?` `DateTime` `DateTime?` `TimeSpan` `TimeSpan?` `GUID` `GUID?` ,,,,,, e.

## <a name="example-cast-for-an-attribute-in-a-namespace"></a>Exemplo: conversão para um atributo em um namespace

O exemplo a seguir mostra o mesmo código para um atributo que está em um namespace. Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

```csharp
XNamespace aw = "http://www.adventure-works.com";
XElement cust = new XElement(aw + "PhoneNumbers",
    new XElement(aw + "Phone",
        new XAttribute(aw + "type", "home"),
        "555-555-5555"),
    new XElement(aw + "Phone",
        new XAttribute(aw + "type", "work"),
        "555-555-6666")
);
IEnumerable<XElement> elList =
    from el in cust.Descendants(aw + "Phone")
    select el;
foreach (XElement el in elList)
    Console.WriteLine((string)el.Attribute(aw + "type"));
```

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim cust As XElement = _
            <aw:PhoneNumbers>
                <aw:Phone aw:type="home">555-555-5555</aw:Phone>
                <aw:Phone aw:type="work">555-555-6666</aw:Phone>
            </aw:PhoneNumbers>
        Dim elList As IEnumerable(Of XElement) = _
            From el In cust...<aw:Phone> _
            Select el
        For Each el As XElement In elList
            Console.WriteLine(el.@aw:type)
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
home
work
```

## <a name="see-also"></a>Confira também

- [Visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md)
