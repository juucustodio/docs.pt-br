---
title: Visão geral da classe XElement
description: A classe XElement representa elementos XML. Você pode usá-lo para criar e alterar elementos, adicionar atributos e filhos e serializar.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 2b9f0cd8-a1d1-4037-accf-0f38a410fa11
ms.openlocfilehash: 325afd09661532fe44aecf89fe9784520274638e
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551921"
---
# <a name="xelement-class-overview"></a>Visão geral da classe XElement

A <xref:System.Xml.Linq.XElement> classe é uma das classes fundamentais em LINQ to XML. Representa um elemento XML. A lista a seguir mostra como você pode usar essa classe para:

- Criar elementos.
- Altere o conteúdo do elemento.
- Adicionar, alterar ou excluir elementos filho.
- Adicionar atributos a um elemento.
- Serialize o conteúdo de um elemento na forma de texto.

Você também pode interoperar com outras classes no <xref:System.Xml?displayProperty=nameWithType>, como <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> e <xref:System.Xml.Xsl.XslCompiledTransform>.

Este artigo descreve a funcionalidade fornecida pela <xref:System.Xml.Linq.XElement> classe.

## <a name="construct-xml-trees"></a>Construir árvores XML

Você pode construir árvores XML de maneiras diferentes, incluindo as seguintes:

- Você pode construir uma árvore XML em código. Para obter mais informações, consulte [árvores XML](functional-construction.md).
- Você pode analisar XML de várias fontes, incluindo <xref:System.IO.TextReader>, arquivos de texto ou um endereço Web (URL). Para obter mais informações, consulte [Parse XML](parse-string.md).
- Você pode usar um <xref:System.Xml.XmlReader> para popular a árvore. Para obter mais informações, consulte <xref:System.Xml.Linq.XNode.ReadFrom%2A>.
- Se você tiver um módulo que possa gravar conteúdo em um <xref:System.Xml.XmlWriter> , poderá usar o <xref:System.Xml.Linq.XContainer.CreateWriter%2A> método para criar um gravador, passar o gravador para o módulo e, em seguida, usar o conteúdo que é gravado no <xref:System.Xml.XmlWriter> para popular a árvore XML.

O exemplo a seguir cria uma árvore. A versão C# usa criações de elemento aninhado. Você pode usar a mesma técnica em Visual Basic, mas este exemplo usa literais XML.

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

Você também pode usar uma consulta LINQ to XML para popular uma árvore XML, conforme mostrado no exemplo a seguir:

```csharp
XElement srcTree = new XElement("Root",
    new XElement("Element", 1),
    new XElement("Element", 2),
    new XElement("Element", 3),
    new XElement("Element", 4),
    new XElement("Element", 5)
);
XElement xmlTree = new XElement("Root",
    new XElement("Child", 1),
    new XElement("Child", 2),
    from el in srcTree.Elements()
    where (int)el > 2
    select el
);
Console.WriteLine(xmlTree);
```

```vb
Dim srcTree As XElement = _
    <Root>
        <Element>1</Element>
        <Element>2</Element>
        <Element>3</Element>
        <Element>4</Element>
        <Element>5</Element>
    </Root>
Dim xmlTree As XElement = _
    <Root>
        <Child>1</Child>
        <Child>2</Child>
        <%= From el In srcTree.Elements() _
            Where el.Value > 2 _
            Select el %>
    </Root>
Console.WriteLine(xmlTree)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Child>1</Child>
  <Child>2</Child>
  <Element>3</Element>
  <Element>4</Element>
  <Element>5</Element>
</Root>
```

## <a name="serialize-xml-trees"></a>Serializar árvores XML

Você pode serializar a árvore XML para um <xref:System.IO.File>, um <xref:System.IO.TextWriter> ou um <xref:System.Xml.XmlWriter>.

Para obter mais informações, consulte [Serialize árvores XML](preserve-white-space-serializing.md).

## <a name="retrieve-xml-data-via-axis-methods"></a>Recuperar dados XML por meio de métodos de eixo

Você pode usar métodos de eixo para recuperar atributos, elementos filho, elementos descendentes e elementos ancestrais. LINQ to XML consultas operam em métodos de eixo e fornecem várias maneiras flexíveis e poderosas de navegar e processar uma árvore XML.

Para obter mais informações, consulte [visão geral dos eixos de LINQ to XML](linq-xml-axes-overview.md).

## <a name="query-xml-trees"></a>Consultar árvores XML

Você pode escrever LINQ to XML consultas que extraem dados de uma árvore XML.

Para obter mais informações, consulte [visão geral das árvores XML de consulta](query-xml-trees-overview.md).

## <a name="modify-xml-trees"></a>Modificar árvores XML

Você pode modificar um elemento de diferentes maneiras, incluindo a alteração de seu conteúdo ou atributos. Você também pode remover um elemento de seu pai.

Para obter mais informações, consulte [Modify XML Trees](in-memory-xml-tree-modification-vs-functional-construction.md).

## <a name="see-also"></a>Confira também

- [Visão geral da programação de LINQ to XML](functional-vs-procedural-programming.md)
