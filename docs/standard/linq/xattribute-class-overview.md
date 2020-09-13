---
title: Visão geral da classe XAttribute
description: A classe XAttribute representa atributos XML. Trabalhar com atributos em LINQ to XML é semelhante a trabalhar com elementos.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 5a630f24-f9ad-400e-831e-c14ebfc9e142
ms.openlocfilehash: deab6e8dd9695a442cd362401aec8b68cdbf218f
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551860"
---
# <a name="xattribute-class-overview"></a>Visão geral da classe XAttribute

Os atributos são pares de nome-valor associados a um elemento. A classe de <xref:System.Xml.Linq.XAttribute> representa atributos XML.

Trabalhar com atributos em LINQ to XML é semelhante a trabalhar com elementos. Os construtores são semelhantes. Os métodos que você usa para recuperar coleções deless são semelhantes. Uma expressão de consulta LINQ para uma coleção de atributos é semelhante a uma expressão de consulta LINQ para uma coleção de elementos.

A ordem em que os atributos foram adicionados a um elemento é preservada. Isto é, quando você itera através de atributos, você ver na mesma ordem que foram adicionados.

## <a name="the-xattribute-constructor"></a>O Construtor XAttribute

O seguinte construtor da <xref:System.Xml.Linq.XAttribute> classe é aquele que você usará com mais frequência:

|Construtor|Descrição|
|-----------------|-----------------|
|`XAttribute(XName name, object content)`|Cria um objeto de <xref:System.Xml.Linq.XAttribute> . O argumento de `name` especifica o nome do atributo; `content` especifica o conteúdo de atributo.|

## <a name="example-create-an-element-with-an-attribute"></a>Exemplo: criar um elemento com um atributo

O exemplo a seguir mostra a tarefa comum de criar um elemento que contém um atributo.

```csharp
XElement phone = new XElement("Phone",
    new XAttribute("Type", "Home"),
    "555-555-5555");
Console.WriteLine(phone);
```

```vb
Dim phone As XElement = <Phone Type="Home">555-555-5555</Phone>
Console.WriteLine(phone)
```

Esse exemplo gera a saída a seguir:

```xml
<Phone Type="Home">555-555-5555</Phone>
```

## <a name="example-functional-construction-of-attributes"></a>Exemplo: construção funcional de atributos

Você pode construir <xref:System.Xml.Linq.XAttribute> objetos em linha com a construção de <xref:System.Xml.Linq.XElement> objetos, conforme mostrado no exemplo a seguir:

```csharp
XElement c = new XElement("Customers",
    new XElement("Customer",
        new XElement("Name", "John Doe"),
        new XElement("PhoneNumbers",
            new XElement("Phone",
                new XAttribute("type", "home"),
                "555-555-5555"),
            new XElement("Phone",
                new XAttribute("type", "work"),
                "666-666-6666")
        )
    )
);
Console.WriteLine(c);
```

```vb
Dim c As XElement = _
    <Customers>
        <Customer>
            <Name>John Doe</Name>
            <PhoneNumbers>
                <Phone type="home">555-555-5555</Phone>
                <Phone type="work">666-666-6666</Phone>
            </PhoneNumbers>
        </Customer>
    </Customers>
Console.WriteLine(c)
```

Esse exemplo gera a saída a seguir:

```xml
<Customers>
  <Customer>
    <Name>John Doe</Name>
    <PhoneNumbers>
      <Phone type="home">555-555-5555</Phone>
      <Phone type="work">666-666-6666</Phone>
    </PhoneNumbers>
  </Customer>
</Customers>
```

## <a name="attributes-arent-nodes"></a>Atributos não são nós

Há algumas diferenças entre atributos e elementos. <xref:System.Xml.Linq.XAttribute> objetos não são nós na árvore XML. Eles são pares de nome-valor associados a um elemento XML. Em contraste com Document Object Model (DOM), este reflete mais apertadamente a estrutura XML. Embora os <xref:System.Xml.Linq.XAttribute> objetos não sejam realmente nós na árvore XML, trabalhar com <xref:System.Xml.Linq.XAttribute> objetos é semelhante a trabalhar com <xref:System.Xml.Linq.XElement> objetos.

Essa distinção importante é primeiro somente para os desenvolvedores que estão escrevendo código que funciona com as árvores XML no nível do nó. Muitos desenvolvedores não se preocupam com essa distinção.

## <a name="see-also"></a>Confira também

- [Visão geral de LINQ to XML](linq-xml-overview.md)
