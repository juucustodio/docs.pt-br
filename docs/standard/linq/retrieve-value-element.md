---
title: Como recuperar o valor de um elemento-LINQ to XML
description: 'Conheça as duas maneiras principais de obter o valor de um elemento ou atributo: Converta para o tipo desejado ou use as propriedades XElement. Value e XAttribute. Value.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4228c007-07c9-4cf2-a45b-e7074c109581
ms.openlocfilehash: 010af5db9ec991bfe0345c93def3241150aa15e2
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552055"
---
# <a name="how-to-retrieve-the-value-of-an-element-linq-to-xml"></a>Como recuperar o valor de um elemento (LINQ to XML)

Este artigo mostra como obter o valor dos elementos. Há duas maneiras principais de obter o valor:

- Converta um <xref:System.Xml.Linq.XElement> ou um <xref:System.Xml.Linq.XAttribute> para o tipo desejado. O operador de conversão explícita converte o conteúdo do elemento ou do atributo no tipo especificado e o atribui à sua variável.

- Use as <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=nameWithType> Propriedades ou. Você também pode definir o valor usando essas propriedades.

Com o C#, a conversão é geralmente a melhor abordagem. Se você converter o elemento ou atributo em um tipo de valor anulável, o código será mais simples de escrever ao recuperar o valor de um elemento (ou atributo) que pode não existir. O último exemplo neste artigo demonstra isso. No entanto, você não pode definir o conteúdo de um elemento por meio de conversão, como é possível através da <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> propriedade.

Com Visual Basic, a melhor abordagem é usar a <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> propriedade.

## <a name="string-cast-example"></a>Exemplo de conversão de cadeia de caracteres  

Para recuperar o valor de um elemento, converta o <xref:System.Xml.Linq.XElement> objeto para o tipo desejado. Você pode converter um elemento em uma cadeia de caracteres da seguinte maneira:

```csharp
XElement e = new XElement("StringElement", "abcde");
Console.WriteLine(e);
Console.WriteLine("Value of e:" + (string)e);
```

```vb
Dim e As XElement = <StringElement>abcde</StringElement>
Console.WriteLine(e)
Console.WriteLine("Value of e:" & e.Value)
```

Esse exemplo gera a saída a seguir:

```output
<StringElement>abcde</StringElement>
Value of e:abcde
```

## <a name="integer-cast-example"></a>Exemplo de conversão de inteiro  

Você também pode converter elementos em tipos que não sejam cadeias de caracteres. Por exemplo, se você tiver um elemento que contenha um número inteiro, poderá convertê-lo em `int`, como mostrado no código a seguir:  

```csharp
XElement e = new XElement("Age", "44");
Console.WriteLine(e);
Console.WriteLine("Value of e:" + (int)e);
```

```vb
Dim e As XElement = <Age>44</Age>
Console.WriteLine(e)
Console.WriteLine("Value of e:" & CInt(e))
```

Esse exemplo gera a saída a seguir:

```output
<Age>44</Age>
Value of e:44
```

LINQ to XML fornece operadores de conversão explícitos para os seguintes tipos de dados:,,,,,,, `string` `bool` `bool?` `int` `int?` `uint` `uint?` `long` , `long?` , `ulong` , `ulong?` , `float` , `float?` , `double` , `double?` , `decimal` , `decimal?` , `DateTime` , `DateTime?` , `TimeSpan` , `TimeSpan?` , `GUID` e `GUID?` .

LINQ to XML fornece os mesmos operadores de conversão para <xref:System.Xml.Linq.XAttribute> objetos.

## <a name="value-property-example"></a>Exemplo da propriedade Value

É possível usar a propriedade <xref:System.Xml.Linq.XElement.Value%2A> para recuperar o conteúdo de um elemento:

```csharp
XElement e = new XElement("StringElement", "abcde");
Console.WriteLine(e);
Console.WriteLine("Value of e:" + e.Value);
```

```vb
Dim e As XElement = <StringElement>abcde</StringElement>
Console.WriteLine(e)
Console.WriteLine("Value of e:" & e.Value)
```

Esse exemplo gera a saída a seguir:

```output
<StringElement>abcde</StringElement>
Value of e:abcde
```

## <a name="element-might-not-exist-example"></a>O elemento pode não existir exemplo

Às vezes você tenta recuperar o valor de um elemento, mesmo que não tenha certeza se ele existe. Nesse caso, quando você atribui o elemento convertido a um tipo de referência anulável ou tipo de valor anulável, se o elemento não existir, a variável atribuída será definida como `null` (C#) ou `nothing` (Visual Basic). O código a seguir mostra que, quando o elemento pode não existir, é mais fácil usar a conversão do que usar a <xref:System.Xml.Linq.XElement.Value%2A> propriedade.

```csharp
XElement root = new XElement("Root",
    new XElement("Child1", "child 1 content"),
    new XElement("Child2", "2")
);

// The following assignments show why it's easier to use
// casting when the element might or might not exist.

string c1 = (string)root.Element("Child1");
Console.WriteLine("c1:{0}", c1 == null ? "element doesn't exist" : c1);

int? c2 = (int?)root.Element("Child2");
Console.WriteLine("c2:{0}", c2 == null ? "element doesn't exist" : c2.ToString());

string c3 = (string)root.Element("Child3");
Console.WriteLine("c3:{0}", c3 == null ? "element doesn't exist" : c3);

int? c4 = (int?)root.Element("Child4");
Console.WriteLine("c4:{0}", c4 == null ? "element doesn't exist" : c4.ToString());

Console.WriteLine();

// The following assignments show the required code when using
// the Value property when the element might or might not exist.
// Notice that this is more difficult than the casting approach.

XElement e1 = root.Element("Child1");
string v1;
if (e1 == null)
    v1 = null;
else
    v1 = e1.Value;
Console.WriteLine("v1:{0}", v1 == null ? "element doesn't exist" : v1);

XElement e2 = root.Element("Child2");
int? v2;
if (e2 == null)
    v2 = null;
else
    v2 = Int32.Parse(e2.Value);
Console.WriteLine("v2:{0}", v2 == null ? "element doesn't exist" : v2.ToString());

XElement e3 = root.Element("Child3");
string v3;
if (e3 == null)
    v3 = null;
else
    v3 = e3.Value;
Console.WriteLine("v3:{0}", v3 == null ? "element doesn't exist" : v3);

XElement e4 = root.Element("Child4");
int? v4;
if (e4 == null)
    v4 = null;
else
    v4 = Int32.Parse(e4.Value);
Console.WriteLine("v4:{0}", v4 == null ? "element doesn't exist" : v4.ToString());
```

```vb
Dim root As XElement = <Root>
                           <Child1>child 1 content</Child1>
                           <Child2>2</Child2>
                       </Root>

' The following assignments show why it's easier to use
' casting when the element might or might not exist.

Dim c1 As String = CStr(root.Element("Child1"))
Console.WriteLine("c1:{0}", IIf(c1 Is Nothing, "element doesn't exist", c1))

Dim c2 As Nullable(Of Integer) = CType(root.Element("Child2"), Nullable(Of Integer))
Console.WriteLine("c2:{0}", IIf(Not (c2.HasValue), "element doesn't exist", c2.ToString()))

Dim c3 As String = CStr(root.Element("Child3"))
Console.WriteLine("c3:{0}", IIf(c3 Is Nothing, "element doesn't exist", c3))

Dim c4 As Nullable(Of Integer) = CType(root.Element("Child4"), Nullable(Of Integer))
Console.WriteLine("c4:{0}", IIf(Not (c4.HasValue), "element doesn't exist", c4.ToString()))

Console.WriteLine()

' The following assignments show the required code when using
' the Value property when the attribute might or might not exist.
' Notice that this is more difficult than the casting approach.

Dim e1 As XElement = root.Element("Child1")
Dim v1 As String
If (e1 Is Nothing) Then
    v1 = Nothing
Else
    v1 = e1.Value
End If
Console.WriteLine("v1:{0}", IIf(v1 Is Nothing, "element doesn't exist", v1))

Dim e2 As XElement = root.Element("Child2")
Dim v2 As Nullable(Of Integer)
If (e2 Is Nothing) Then
    v2 = Nothing
Else
    v2 = e2.Value
End If
Console.WriteLine("v2:{0}", IIf(Not (v2.HasValue), "element doesn't exist", v2))

Dim e3 As XElement = root.Element("Child3")
Dim v3 As String
If (e3 Is Nothing) Then
    v3 = Nothing
Else
    v3 = e3.Value
End If
Console.WriteLine("v3:{0}", IIf(v3 Is Nothing, "element doesn't exist", v3))

Dim e4 As XElement = root.Element("Child4")
Dim v4 As Nullable(Of Integer)
If (e4 Is Nothing) Then
    v4 = Nothing
Else
    v4 = e4.Value
End If
Console.WriteLine("v4:{0}", IIf(Not (v4.HasValue), "element doesn't exist", v4))
```

Esse exemplo gera a saída a seguir:

```output
c1:child 1 content
c2:2
c3:element doesn't exist
c4:element doesn't exist

v1:child 1 content
v2:2
v3:element doesn't exist
v4:element doesn't exist
```

Em geral, você pode escrever um código mais simples por meio da conversão para recuperar o conteúdo de elementos e atributos.

## <a name="see-also"></a>Confira também

- [Visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md)
