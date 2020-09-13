---
title: Como recuperar o valor superficial de um elemento-LINQ to XML
description: Use o `ShallowValue` método de extensão para recuperar o valor superficial de um elemento. O valor superficial é o valor somente daquele elemento; ou seja, ele não inclui os valores de elementos descendentes.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 924a2699-72f6-4be1-aaa6-de62f8ec73b9
ms.openlocfilehash: 761ffc07b13ebdc652b75bf96ba5b121c7912fd7
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552061"
---
# <a name="how-to-retrieve-the-shallow-value-of-an-element-linq-to-xml"></a>Como recuperar o valor superficial de um elemento (LINQ to XML)

Este artigo mostra como recuperar o valor superficial de um elemento, que é o valor somente daquele elemento, não incluindo valores de elementos descendentes. Recuperar o valor raso é útil quando você deseja selecionar elementos com base no conteúdo.

Quando você usa a conversão ou a <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> propriedade para recuperar um valor de elemento, o valor inclui os descendentes. Para recuperar o valor superficial, você pode usar o `ShallowValue` método de extensão, conforme mostrado no exemplo a seguir. O exemplo declara um método de extensão que recupera o valor superficial de um elemento. Use o método de extensão em uma consulta para listar todos os elementos que contém um valor calculado.

## <a name="example-use-the-shallowvalue-extension-method-to-retrieve-the-shallow-value-of-an-element"></a>Exemplo: usar o `ShallowValue` método de extensão para recuperar o valor superficial de um elemento

Os exemplos usam o arquivo de texto Report.xml que contém o seguinte:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Report>
  <Section>
    <Heading>
      <Column Name="CustomerId">=Customer.CustomerId.Heading</Column>
      <Column Name="Name">=Customer.Name.Heading</Column>
    </Heading>
    <Detail>
      <Column Name="CustomerId">=Customer.CustomerId</Column>
      <Column Name="Name">=Customer.Name</Column>
    </Detail>
  </Section>
</Report>
```

Este é o código para o exemplo:

```csharp
public static class MyExtensions
{
    public static string ShallowValue(this XElement xe)
    {
        return xe
               .Nodes()
               .OfType<XText>()
               .Aggregate(new StringBuilder(),
                          (s, c) => s.Append(c),
                          s => s.ToString());
    }
}

class Program
{
    static void Main(string[] args)
    {
        XElement root = XElement.Load("Report.xml");

        IEnumerable<XElement> query = from el in root.Descendants()
                                      where el.ShallowValue().StartsWith("=")
                                      select el;

        foreach (var q in query)
        {
            Console.WriteLine("{0}{1}{2}",
                q.Name.ToString().PadRight(8),
                q.Attribute("Name").ToString().PadRight(20),
                q.ShallowValue());
        }
    }
}
```

```vb
Module Module1
    <System.Runtime.CompilerServices.Extension()> _
    Public Function ShallowValue(ByVal xe As XElement)
        Return xe _
               .Nodes() _
               .OfType(Of XText)() _
               .Aggregate(New StringBuilder(), _
                              Function(s, c) s.Append(c), _
                              Function(s) s.ToString())
    End Function

    Sub Main()
        Dim root As XElement = XElement.Load("Report.xml")

        Dim query As IEnumerable(Of XElement) = _
            From el In root.Descendants() _
            Where (el.ShallowValue().StartsWith("=")) _
            Select el

        For Each q As XElement In query
            Console.WriteLine("{0}{1}{2}", _
                q.Name.ToString().PadRight(8), _
                q.Attribute("Name").ToString().PadRight(20), _
                q.ShallowValue())
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
Column  Name="CustomerId"   =Customer.CustomerId.Heading
Column  Name="Name"         =Customer.Name.Heading
Column  Name="CustomerId"   =Customer.CustomerId
Column  Name="Name"         =Customer.Name
```

## <a name="see-also"></a>Confira também

- [Visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md)
