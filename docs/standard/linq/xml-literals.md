---
title: Literais XML em Visual Basic-LINQ to XML
description: Você pode criar uma árvore XML em Visual Basic usando literais XML e expressões inseridas. Expressões inseridas permite avaliar uma expressão e para inserir os resultados da expressão na árvore XML.
ms.date: 07/20/2015
ms.assetid: 94fc0e03-978e-4c08-ab6c-0dc3c1e64f10
ms.openlocfilehash: e3b1213672a6a7ddd71fcc38b4502108a6f49881
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551946"
---
# <a name="xml-literals-in-visual-basic-linq-to-xml"></a>Literais XML em Visual Basic (LINQ to XML)

Este artigo fornece informações sobre como criar árvores XML em Visual Basic usando literais XML e expressões inseridas.

## <a name="example-use-xml-literals-to-create-an-xml-tree"></a>Exemplo: usar literais XML para criar uma árvore XML

O exemplo a seguir mostra como criar um <xref:System.Xml.Linq.XElement> , nesse caso `contacts` , com literais XML:

```vb
Dim contacts As XElement = _
    <Contacts>
        <Contact>
            <Name>Patrick Hines</Name>
            <Phone>206-555-0144</Phone>
            <Address>
                <Street1>123 Main St</Street1>
                <City>Mercer Island</City>
                <State>WA</State>
                <Postal>68042</Postal>
            </Address>
        </Contact>
    </Contacts>
```

## <a name="example-use-xml-literals-to-create-an-xelement-with-simple-content"></a>Exemplo: usar literais XML para criar um XElement com conteúdo simples

Você pode criar <xref:System.Xml.Linq.XElement> que contém o conteúdo simples, como segue:

```vb
Dim n as XElement = <Customer>Adventure Works</Customer>
Console.WriteLine(n)
```

Esse exemplo gera a saída a seguir:

```xml
<Customer>Adventure Works</Customer>
```

## <a name="example-use-an-xml-literal-to-create-an-empty-element"></a>Exemplo: usar um literal XML para criar um elemento vazio

Você pode criar <xref:System.Xml.Linq.XElement>vazia, como segue:

```vb
Dim n As XElement = <Customer/>
Console.WriteLine(n)
```

Esse exemplo gera a saída a seguir:

```xml
<Customer />
```

## <a name="use-embedded-expressions-to-create-content"></a>Usar expressões inseridas para criar conteúdo

Um recurso importante de literais XML é que permitem expressões inseridas. Expressões inseridas permite avaliar uma expressão e para inserir os resultados da expressão na árvore XML. Se a expressão avaliada como um tipo de <xref:System.Xml.Linq.XElement>, um elemento é inserido na árvore. Se a expressão avaliada como um tipo de <xref:System.Xml.Linq.XAttribute>, um atributo é inserido na árvore. Você pode inserir elementos e atributos na árvore somente quando eles forem válidos.

é importante observar que apenas uma única expressão pode entrar em uma expressão inserida. Não é possível inserir várias instruções. Se uma expressão ultrapassa de uma única linha, você deve usar o caractere de continuação de linha.

Se você usar uma expressão inserida para adicionar nós existentes (incluindo elementos) e atributos para uma nova árvore XML e os nós existentes já parented, os nós são clonados. Os nós recentemente clonados são anexados a nova árvore XML. Se os nós existentes não forem pais, os nós serão simplesmente anexados à nova árvore XML. O último exemplo neste artigo demonstra isso.

## <a name="example-use-an-embedded-expression-to-insert-an-element"></a>Exemplo: usar uma expressão inserida para inserir um elemento

O exemplo a seguir usa uma expressão inserida para inserir um elemento na árvore:

```vb
xmlTree1 As XElement = _
    <Root>
        <Child>Contents</Child>
    </Root>
Dim xmlTree2 As XElement = _
    <Root>
        <%= xmlTree1.<Child> %>
    </Root>
Console.WriteLine(xmlTree2)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Child>Contents</Child>
</Root>
```

## <a name="example-use-an-embedded-expression-for-content"></a>Exemplo: usar uma expressão inserida para conteúdo

Você pode usar uma expressão inserida para fornecer o conteúdo de um elemento:

```vb
Dim str As String
str = "Some content"
Dim root As XElement = <Root><%= str %></Root>
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>Some content</Root>
```

## <a name="example-use-a-linq-query-in-an-embedded-expression"></a>Exemplo: usar uma consulta LINQ em uma expressão inserida

Você pode usar os resultados de uma consulta LINQ para fornecer o conteúdo de um elemento:

```vb
Dim arr As Integer() = {1, 2, 3}

Dim n As XElement = _
    <Root>
        <%= From i In arr Select <Child><%= i %></Child> %>
    </Root>

Console.WriteLine(n)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Child>1</Child>
  <Child>2</Child>
  <Child>3</Child>
</Root>
```

## <a name="example-use-an-embedded-expression-to-provide-node-names"></a>Exemplo: usar uma expressão inserida para fornecer nomes de nós

Você também pode usar uma expressão inserida para calcular nomes de atributo, valores de atributo, nomes de elementos e valores de elementos:

```vb
Dim eleName As String = "ele"
Dim attName As String = "att"
Dim attValue As String = "aValue"
Dim eleValue As String = "eValue"
Dim n As XElement = _
    <Root <%= attName %>=<%= attValue %>>
        <<%= eleName %>>
            <%= eleValue %>
        </>
    </Root>
Console.WriteLine(n)
```

Esse exemplo gera a saída a seguir:

```xml
<Root att="aValue">
  <ele>eValue</ele>
</Root>
```

## <a name="example-use-an-embedded-expression-to-clone-and-attach-nodes"></a>Exemplo: usar uma expressão inserida para clonar e anexar nós

Como mencionado anteriormente, se você usar uma expressão inserida para adicionar nós existentes (incluindo elementos) e atributos a uma nova árvore XML, e se os nós que estão sendo adicionados a nós já estiverem pais, os nós serão clonados e os clones serão anexados à nova árvore XML. Se os nós existentes não forem pais, eles serão simplesmente anexados à nova árvore XML.

O código a seguir demonstra o comportamento quando você adiciona um elemento parented a uma árvore, e quando você adiciona um elemento sem o pai a uma árvore.

```vb
' Create a tree with a child element.
Dim xmlTree1 As XElement = _
    <Root>
        <Child1>1</Child1>
    </Root>

' Create an element that's not parented.
Dim child2 As XElement = <Child2>2</Child2>

' Create a tree and add Child1 and Child2 to it.
Dim xmlTree2 As XElement = _
    <Root>
        <%= xmlTree1.<Child1>(0) %>
        <%= child2 %>
    </Root>

' Compare Child1 identity.
Console.WriteLine("Child1 was {0}", _
    IIf(xmlTree1.Element("Child1") Is xmlTree2.Element("Child1"), _
    "attached", "cloned"))

' Compare Child2 identity.
Console.WriteLine("Child2 was {0}", _
    IIf(child2 Is xmlTree2.Element("Child2"), _
    "attached", "cloned"))
```

Esse exemplo gera a saída a seguir:

```output
Child1 was cloned
Child2 was attached
```

## <a name="see-also"></a>Confira também

- [Construção funcional](functional-construction.md)
