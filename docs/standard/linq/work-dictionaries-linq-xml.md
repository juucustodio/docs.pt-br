---
title: Como trabalhar com dicionários usando LINQ to XML-LINQ to XML
description: Você pode converter muitos tipos de estruturas de dados em XML e pode converter XML em estruturas. Aqui está um exemplo que converte um. Dictionary genérico em XML e vice-versa.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 57bcefe3-8433-4d3b-935a-511c9bcbdfa8
ms.openlocfilehash: ea61a79549488765526f45852dae7a4df7cacb64
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551948"
---
# <a name="how-to-work-with-dictionaries-using-linq-to-xml"></a>Como trabalhar com dicionários usando LINQ to XML

Geralmente, é conveniente converter as estruturas de dados de vários tipos em XML e, em seguida, de XML para outras estruturas de dados. Este artigo mostra uma conversão de um <xref:System.Collections.Generic.Dictionary%602> para XML e de volta.

## <a name="example-create-a-dictionary-and-convert-its-contents-to-xml"></a>Exemplo: criar um dicionário e converter seu conteúdo em XML

Este primeiro exemplo cria um <xref:System.Collections.Generic.Dictionary%602> e, em seguida, converte-o em XML.

Esta versão C# do exemplo usa uma forma de construção funcional em que uma consulta projeta novos <xref:System.Xml.Linq.XElement> objetos e a coleção resultante é passada como um argumento para o construtor do <xref:System.Xml.Linq.XElement> objeto raiz.

A versão Visual Basic usa literais XML e uma consulta em uma expressão inserida. A consulta projeta novos <xref:System.Xml.Linq.XElement> objetos que se tornam o novo conteúdo do `Root` <xref:System.Xml.Linq.XElement> objeto.

```csharp
Dictionary<string, string> dict = new Dictionary<string, string>();
dict.Add("Child1", "Value1");
dict.Add("Child2", "Value2");
dict.Add("Child3", "Value3");
dict.Add("Child4", "Value4");
XElement root = new XElement("Root",
    from keyValue in dict
    select new XElement(keyValue.Key, keyValue.Value)
);
Console.WriteLine(root);
```

```vb
Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)()
dict.Add("Child1", "Value1")
dict.Add("Child2", "Value2")
dict.Add("Child3", "Value3")
dict.Add("Child4", "Value4")
Dim root As XElement = _
    <Root>
        <%= From keyValue In dict _
            Select New XElement(keyValue.Key, keyValue.Value) %>
    </Root>
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Child1>Value1</Child1>
  <Child2>Value2</Child2>
  <Child3>Value3</Child3>
  <Child4>Value4</Child4>
</Root>
```

## <a name="example-create-a-dictionary-and-load-it-from-xml-data"></a>Exemplo: criar um dicionário e carregá-lo a partir de dados XML

O exemplo a seguir cria uma carga de dicionário carregada a partir de dados XML.

```csharp
XElement root = new XElement("Root",
    new XElement("Child1", "Value1"),
    new XElement("Child2", "Value2"),
    new XElement("Child3", "Value3"),
    new XElement("Child4", "Value4")
);

Dictionary<string, string> dict = new Dictionary<string, string>();
foreach (XElement el in root.Elements())
    dict.Add(el.Name.LocalName, el.Value);
foreach (string str in dict.Keys)
    Console.WriteLine("{0}:{1}", str, dict[str]);
```

```vb
Dim root As XElement = _
        <Root>
            <Child1>Value1</Child1>
            <Child2>Value2</Child2>
            <Child3>Value3</Child3>
            <Child4>Value4</Child4>
        </Root>

Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)
For Each el As XElement In root.Elements
    dict.Add(el.Name.LocalName, el.Value)
Next
For Each str As String In dict.Keys
    Console.WriteLine("{0}:{1}", str, dict(str))
Next
```

Esse exemplo gera a saída a seguir:

```output
Child1:Value1
Child2:Value2
Child3:Value3
Child4:Value4
```

## <a name="see-also"></a>Confira também

- [Projeções e transformações (LINQ to XML) (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
