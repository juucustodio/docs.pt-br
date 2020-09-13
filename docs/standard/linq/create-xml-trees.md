---
title: Criar árvores XML em C#-LINQ to XML
description: Você pode criar uma árvore XML em C# usando os construtores LINQ to XML XElement e XAttribute, e pode fazer com que o código se assemelhe à estrutura do XML subjacente.
ms.date: 08/31/2018
ms.assetid: cc74234a-0bac-4327-9c8c-5a2ead15b595
ms.openlocfilehash: 97bf40d84f40eabf6fa84f10bf4febb7697b10f5
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552300"
---
# <a name="create-xml-trees-in-c-linq-to-xml"></a>Criar árvores XML em C# (LINQ to XML)

Este artigo fornece informações sobre a criação de árvores XML em C#.

Para obter informações sobre como usar os resultados de consultas LINQ como o conteúdo de um <xref:System.Xml.Linq.XElement> , consulte [construção funcional](functional-construction.md).

## <a name="construct-elements"></a>Elementos de construção

As assinaturas dos construtores <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XAttribute> permitem que você passe o conteúdo do elemento ou atributo como argumentos para o construtor. Como um dos construtores recebe um número variável de argumentos, você pode passar qualquer número de elementos filhos. Naturalmente, cada um desses elementos filhos pode conter seus próprios elementos filhos. Para qualquer elemento, você pode adicionar a quantidade desejada de atributos.

Ao adicionar objetos <xref:System.Xml.Linq.XNode> (inclusive <xref:System.Xml.Linq.XElement>) ou <xref:System.Xml.Linq.XAttribute>, se o novo conteúdo não tiver um pai, os objetos serão simplesmente anexados à árvore XML. Se o novo conteúdo já tiver um pai e fizer parte de outra árvore XML, o novo conteúdo será clonado, e o conteúdo recém-clonado será anexado à árvore XML. O último exemplo neste artigo demonstra isso.

Para criar um `contacts` <xref:System.Xml.Linq.XElement> , você pode usar o seguinte código:

```csharp
XElement contacts =
    new XElement("Contacts",
        new XElement("Contact",
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),
            new XElement("Address",
                new XElement("Street1", "123 Main St"),
                new XElement("City", "Mercer Island"),
                new XElement("State", "WA"),
                new XElement("Postal", "68042")
            )
        )
    );
```

Se recuado corretamente, o código para criar objetos <xref:System.Xml.Linq.XElement> é muito parecido com a estrutura do XML subjacente.

## <a name="xelement-constructors"></a>Construtores de XElement

A classe <xref:System.Xml.Linq.XElement> usa os seguintes construtores na construção funcional. Observe que há alguns outros construtores para o <xref:System.Xml.Linq.XElement> , mas como eles não são usados para a construção funcional, eles não estão listados aqui.

|Construtor|Descrição|
|-----------------|-----------------|
|`XElement(XName name, object content)`|Cria um <xref:System.Xml.Linq.XElement>. O parâmetro `name` especifica o nome do elemento; `content` especifica o conteúdo do elemento.|
|`XElement(XName name)`|Cria um <xref:System.Xml.Linq.XElement> com seu <xref:System.Xml.Linq.XName> inicializado para o nome especificado.|
|`XElement(XName name, params object[] content)`|Cria um <xref:System.Xml.Linq.XElement> com seu <xref:System.Xml.Linq.XName> inicializado para o nome especificado. Os atributos e/ou elementos filhos são criados a partir do conteúdo da lista de parâmetros.|

O parâmetro `content` é muito flexível. Ele dá suporte a qualquer tipo de objeto que seja um filho válido de um <xref:System.Xml.Linq.XElement> . As seguintes regras se aplicam aos diferentes tipos de objetos passados neste parâmetro:

- Uma cadeia de caracteres é adicionada como conteúdo de texto.
- Um <xref:System.Xml.Linq.XElement> é adicionado como um elemento filho.
- Um <xref:System.Xml.Linq.XAttribute> é adicionado como um atributo.
- Um <xref:System.Xml.Linq.XProcessingInstruction>, <xref:System.Xml.Linq.XComment> ou <xref:System.Xml.Linq.XText> é adicionado como conteúdo filho.
- Um <xref:System.Collections.IEnumerable> é enumerado, e essas regras são aplicadas recursivamente aos resultados.
- Para qualquer outro tipo, seu método `ToString` é chamado e o resultado é adicionado como conteúdo de texto.

## <a name="example-create-an-xelement-with-content"></a>Exemplo: criar um XElement com conteúdo

Você pode criar um <xref:System.Xml.Linq.XElement> contendo o conteúdo simples com uma única chamada de método. Para fazer isso, especifique o conteúdo como o segundo parâmetro, como segue:

```csharp
XElement n = new XElement("Customer", "Adventure Works");
Console.WriteLine(n);
```

Esse exemplo gera a saída a seguir:

```xml
<Customer>Adventure Works</Customer>
```

Você pode passar qualquer tipo de objeto como o conteúdo. Por exemplo, o seguinte código cria um elemento que contém um número de ponto flutuante como conteúdo:

```csharp
XElement n = new XElement("Cost", 324.50);
Console.WriteLine(n);
```

Esse exemplo gera a saída a seguir:

```xml
<Cost>324.5</Cost>
```

O número de ponto flutuante foi convertido e passado para o construtor. O número é convertido em uma cadeia de caracteres e usado como o conteúdo do elemento.

## <a name="example-create-an-xelement-with-a-child-element"></a>Exemplo: criar um XElement com um elemento filho

Se você passar uma instância da classe <xref:System.Xml.Linq.XElement> para o argumento de conteúdo, o construtor criará um elemento com um elemento filho:

```csharp
XElement shippingUnit = new XElement("ShippingUnit",
    new XElement("Cost", 324.50)
);
Console.WriteLine(shippingUnit);
```

Esse exemplo gera a saída a seguir:

```xml
<ShippingUnit>
  <Cost>324.5</Cost>
</ShippingUnit>
```

## <a name="example-create-an-xelement-with-multiple-child-elements"></a>Exemplo: criar um XElement com vários elementos filho

Você pode passar um número de objetos <xref:System.Xml.Linq.XElement> para o conteúdo. Cada um dos objetos <xref:System.Xml.Linq.XElement> é incluído como um elemento filho.

```csharp
XElement address = new XElement("Address",
    new XElement("Street1", "123 Main St"),
    new XElement("City", "Mercer Island"),
    new XElement("State", "WA"),
    new XElement("Postal", "68042")
);
Console.WriteLine(address);
```

Esse exemplo gera a saída a seguir:

```xml
<Address>
  <Street1>123 Main St</Street1>
  <City>Mercer Island</City>
  <State>WA</State>
  <Postal>68042</Postal>
</Address>
```

Ao estender o exemplo anterior, você pode criar uma árvore XML inteira, da seguinte maneira:

```csharp
XElement contacts =
    new XElement("Contacts",
        new XElement("Contact",
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),
            new XElement("Address",
                new XElement("Street1", "123 Main St"),
                new XElement("City", "Mercer Island"),
                new XElement("State", "WA"),
                new XElement("Postal", "68042")
            )
        )
    );
Console.WriteLine(contacts);
```

Esse exemplo gera a saída a seguir:

```xml
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

## <a name="example-create-an-xelement-with-an-xattribute"></a>Exemplo: criar um XElement com um XAttribute

Se você passar uma instância da classe <xref:System.Xml.Linq.XAttribute> para o argumento de conteúdo, o construtor criará um elemento com um atributo:

```csharp
XElement phone = new XElement("Phone",
    new XAttribute("Type", "Home"),
    "555-555-5555");
Console.WriteLine(phone);
```

Esse exemplo gera a saída a seguir:

```xml
<Phone Type="Home">555-555-5555</Phone>
```

## <a name="example-create-an-empty-element"></a>Exemplo: criar um elemento vazio

Para criar um vazio <xref:System.Xml.Linq.XElement> , não transmita nenhum conteúdo para o construtor. O seguinte exemplo cria um elemento vazio:

```csharp
XElement n = new XElement("Customer");
Console.WriteLine(n);
```

Esse exemplo gera a saída a seguir:

```xml
<Customer />
```

## <a name="example-attach-vs-clone"></a>Exemplo: Attach vs. Clone

Conforme citado anteriormente, ao adicionar objetos <xref:System.Xml.Linq.XNode> (inclusive <xref:System.Xml.Linq.XElement>) ou <xref:System.Xml.Linq.XAttribute>, se o novo conteúdo não tiver um pai, os objetos serão simplesmente anexados à árvore XML. Se o novo conteúdo já tiver um pai e fizer parte de outra árvore XML, o novo conteúdo será clonado, e o conteúdo recém-clonado será anexado à árvore XML.

O exemplo a seguir demonstra o comportamento quando você adiciona um elemento pai a uma árvore e quando você adiciona um elemento sem pai a uma árvore:

```csharp
// Create a tree with a child element.
XElement xmlTree1 = new XElement("Root",
    new XElement("Child1", 1)
);

// Create an element that's not parented.
XElement child2 = new XElement("Child2", 2);

// Create a tree and add Child1 and Child2 to it.
XElement xmlTree2 = new XElement("Root",
    xmlTree1.Element("Child1"),
    child2
);

// Compare Child1 identity.
Console.WriteLine("Child1 was {0}",
    xmlTree1.Element("Child1") == xmlTree2.Element("Child1") ?
    "attached" : "cloned");

// Compare Child2 identity.
Console.WriteLine("Child2 was {0}",
    child2 == xmlTree2.Element("Child2") ?
    "attached" : "cloned");

// This example produces the following output:
//    Child1 was cloned
//    Child2 was attached
```

## <a name="see-also"></a>Confira também

- [Construção funcional](functional-construction.md)
