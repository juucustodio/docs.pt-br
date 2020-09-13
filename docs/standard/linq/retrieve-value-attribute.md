---
title: Como recuperar o valor de um atributo-LINQ to XML
description: Recupere o valor de um atributo. Você pode converter um XAttribute para o tipo desejado ou usar a Propriedade XAttribute. Value.
ms.date: 07/20/2015
ms.assetid: 817bbe89-5979-4234-bf0c-46f63692ac8c
ms.openlocfilehash: 7af3616c9808cad5dfb52f53c74b21a59da5c954
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552057"
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml"></a>Como recuperar o valor de um atributo (LINQ to XML)

Este artigo mostra como obter o valor de atributos. Existem duas maneiras principais: converter <xref:System.Xml.Linq.XAttribute> no tipo desejado; o operador de conversão explícita converte o conteúdo do elemento ou do atributo no tipo especificado. Outra opção é usar a propriedade <xref:System.Xml.Linq.XAttribute.Value%2A>. No entanto, a conversão geralmente é a abordagem recomendada. Se você converter o atributo para um tipo de valor anulável, o código será mais simples de escrever ao recuperar o valor de um atributo que pode ou não existir. Para obter exemplos dessa técnica, consulte [como recuperar o valor de um elemento](retrieve-value-element.md).

## <a name="example-use-a-cast-to-retrieve-the-value-of-an-attribute"></a>Exemplo: usar uma conversão para recuperar o valor de um atributo

Para recuperar o valor de um atributo em C#, você converte o <xref:System.Xml.Linq.XAttribute> objeto para o tipo desejado. No Visual Basic, você pode usar a propriedade de atributo integrado para recuperar o valor.

```csharp
XElement root = new XElement("Root",
                    new XAttribute("Attr", "abcde")
                );
Console.WriteLine(root);
string str = (string)root.Attribute("Attr");
Console.WriteLine(str);
```

```vb
Dim root As XElement = <Root Attr="abcde"/>
Console.WriteLine(root)
Dim str As String = root.@Attr
Console.WriteLine(str)
```

Esse exemplo gera a saída a seguir:

```output
<Root Attr="abcde" />
abcde
```

## <a name="example-use-a-cast-to-retrieve-from-xml-thats-in-a-namespace"></a>Exemplo: usar uma conversão para recuperar do XML que está em um namespace

O exemplo a seguir mostra como recuperar o valor de um atributo se o atributo estiver em um namespace. Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

```csharp
XNamespace aw = "http://www.adventure-works.com";
XElement root = new XElement(aw + "Root",
                    new XAttribute(aw + "Attr", "abcde")
                );
string str = (string)root.Attribute(aw + "Attr");
Console.WriteLine(str);
```

```vb
Imports <xmlns:aw="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = <aw:Root aw:Attr="abcde"/>
        Dim str As String = root.@aw:Attr
        Console.WriteLine(str)
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
abcde
```

## <a name="see-also"></a>Confira também

- [Visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md)
