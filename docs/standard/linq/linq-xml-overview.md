---
title: Visão geral-LINQ to XML
description: O LINQ to XML fornece uma interface de programação XML na memória que é baseada em recursos do .NET e comparável a uma API DOM atualizada.
ms.date: 10/30/2018
dev_langs:
- csharp
- vb
ms.assetid: 716b94d3-0091-4de1-8e05-41bc069fa9dd
ms.openlocfilehash: f805d757c9059a07988c6cb16e41ffed017fe853
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551983"
---
# <a name="linq-to-xml-overview"></a>Visão geral de LINQ to XML

O LINQ to XML fornece uma interface de programação XML na memória que aproveita a .NET LINQ (Consulta Integrada à Linguagem) Framework. O LINQ to XML usa os recursos do .NET e pode ser comparado a uma interface de programação XML de Modelo de Objeto do Documento (DOM) atualizada e reprojetada.

O XML tem sido amplamente adotado como um modo de formatar dados em muitos contextos. Por exemplo, você pode encontrar XML na Web, em arquivos de configuração, em arquivos do Microsoft Office Word e em bancos de dados.

LINQ to XML é uma abordagem atualizada e reprojetada para programação com XML. Ele fornece os recursos de modificação de documentos na memória do Modelo de Objeto do Documento (DOM) e oferece suporte a expressões de consulta LINQ. Embora essas expressões de consulta sejam sintaticamente diferentes de XPath, elas oferecem uma funcionalidade semelhante.

## <a name="linq-to-xml-developers"></a>Desenvolvedores de LINQ to XML

LINQ to XML tem como alvo uma variedade de desenvolvedores. Para um desenvolvedor médio que quer apenas fazer algo, LINQ to XML torna o XML mais fácil fornecendo uma experiência de consulta semelhante ao SQL. Com apenas um pouco de estudo, os programadores podem aprender a escrever consultas sucintas e eficientes na linguagem de programação de sua escolha.

Os desenvolvedores profissionais podem usar LINQ to XML para aumentar muito sua produtividade. Com LINQ to XML, eles podem escrever menos código que seja mais expressivo, mais compacto e mais poderoso. Eles podem usar expressões de consulta de vários domínios de dados ao mesmo tempo.

## <a name="linq-to-xml-is-an-xml-programming-interface"></a>LINQ to XML é uma interface de programação XML

O LINQ to XML é uma interface de programação XML na memória, habilitada para LINQ, que permite trabalhar com XML de dentro das linguagens de programação .NET.

LINQ to XML é como o Modelo de Objeto do Documento (DOM), no qual ele coloca o documento XML na memória. Você pode consultar e modificar o documento e, depois de modificá-lo, pode salvá-lo em um arquivo ou serializá-lo e enviá-lo pela Internet. No entanto, LINQ to XML difere do DOM:

- Ele fornece um novo modelo de objeto que é mais leve e mais fácil de trabalhar.
- Ele aproveita os recursos de linguagem em C# e Visual Basic.

A vantagem mais importante do LINQ to XML é sua integração com LINQ (consulta integrada à linguagem). Essa integração permite que você escreva consultas no documento XML na memória para recuperar coleções de elementos e atributos. O recurso de consulta do LINQ to XML é comparável na funcionalidade (embora não na sintaxe) para XPath e XQuery. A integração do LINQ em C# e Visual Basic fornece digitação mais forte, verificação de tempo de compilação e suporte a depurador aprimorado.

Outra vantagem do LINQ to XML é a capacidade de usar os resultados da consulta como parâmetros para <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XAttribute> construtores de objeto permite uma abordagem poderosa para a criação de árvores XML. Essa abordagem, chamada de *construção funcional*, permite que os desenvolvedores transformem com facilidade árvores XML de uma forma em outra.

Por exemplo, você pode ter uma ordem de compra XML típica, conforme descrito em [arquivo XML de exemplo: ordem de compra típica](sample-xml-file-typical-purchase-order.md). Usando LINQ to XML, você pode executar a consulta a seguir para obter o valor do atributo de número de parte para cada elemento de item na ordem de compra:

```csharp
// Load the XML file from our project directory containing the purchase orders
var filename = "PurchaseOrder.xml";
var currentDirectory = Directory.GetCurrentDirectory();
var purchaseOrderFilepath = Path.Combine(currentDirectory, filename);

XElement purchaseOrder = XElement.Load(purchaseOrderFilepath);

IEnumerable<string> partNos =  from item in purchaseOrder.Descendants("Item")
                               select (string) item.Attribute("PartNumber");
```

```vb
' Load the XML file from our project directory containing the purchase orders
Dim filename = "PurchaseOrder.xml"
Dim currentDirectory = Directory.GetCurrentDirectory()
Dim purchaseOrderFilepath = Path.Combine(currentDirectory, filename)

Dim purchaseOrder As XElement = XElement.Load(purchaseOrderFilepath)

Dim partNos = _
    From item In purchaseOrder...<Item> _
    Select item.@PartNumber
```

Em C#, isso pode ser reescrito no formulário sintaxe de método:

```csharp
IEnumerable<string> partNos = purchaseOrder.Descendants("Item").Select(x => (string) x.Attribute("PartNumber"));
```

Como outro exemplo, você poderia querer uma lista, classificada por número de peça, dos itens com um valor maior que $ 100. Para obter essas informações, você poderia executar a seguinte consulta:

```csharp
// Load the XML file from our project directory containing the purchase orders
var filename = "PurchaseOrder.xml";
var currentDirectory = Directory.GetCurrentDirectory();
var purchaseOrderFilepath = Path.Combine(currentDirectory, filename);

XElement purchaseOrder = XElement.Load(purchaseOrderFilepath);

IEnumerable<XElement> pricesByPartNos =  from item in purchaseOrder.Descendants("Item")
                                 where (int) item.Element("Quantity") * (decimal) item.Element("USPrice") > 100
                                 orderby (string)item.Element("PartNumber")
                                 select item;
```

```vb
' Load the XML file from our project directory containing the purchase orders
Dim filename = "PurchaseOrder.xml"
Dim currentDirectory = Directory.GetCurrentDirectory()
Dim purchaseOrderFilepath = Path.Combine(currentDirectory, filename)

Dim purchaseOrder As XElement = XElement.Load(purchaseOrderFilepath)

Dim partNos = _
From item In purchaseOrder...<Item> _
Where (item.<Quantity>.Value * _
       item.<USPrice>.Value) > 100 _
Order By item.<PartNumber>.Value _
Select item
```

Novamente, em C#, isso pode ser reescrito no formulário sintaxe de método:

```csharp
IEnumerable<XElement> pricesByPartNos = purchaseOrder.Descendants("Item")
                                        .Where(item => (int)item.Element("Quantity") * (decimal)item.Element("USPrice") > 100)
                                        .OrderBy(order => order.Element("PartNumber"));
```

Além desses recursos do LINQ, o LINQ to XML fornece uma interface de programação XML aprimorada. Usando LINQ to XML, você pode:

- Carregar XML de [arquivos](load-xml-file.md) ou [fluxos](stream-xml-fragments-xmlreader.md).
- Serializar o XML em arquivos ou fluxos.
- Crie XML a partir do zero usando a construção funcional.
- Consultar o XML usando eixos do tipo XPath.
- Manipular a árvore XML na memória usando métodos como <xref:System.Xml.Linq.XContainer.Add%2A>, <xref:System.Xml.Linq.XNode.Remove%2A>, <xref:System.Xml.Linq.XNode.ReplaceWith%2A> e <xref:System.Xml.Linq.XElement.SetValue%2A>.
- Validar árvores XML usando XSD.
- Usar uma combinação desses recursos para transformar árvores XML de uma forma em outra.

## <a name="create-xml-trees"></a>Criar árvores XML

Uma das vantagens mais significativas de programação com o LINQ to XML é que é fácil criar árvores XML. Por exemplo, para criar uma árvore XML pequena, você pode escrever código da seguinte forma:

```csharp
XElement contacts =
new XElement("Contacts",
    new XElement("Contact",
        new XElement("Name", "Patrick Hines"),
        new XElement("Phone", "206-555-0144",
            new XAttribute("Type", "Home")),
        new XElement("phone", "425-555-0145",
            new XAttribute("Type", "Work")),
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

> [!NOTE]
> A versão Visual Basic do exemplo usa literais XML. Você também pode usar <xref:System.Xml.Linq.XElement> o no Visual Basic, como na versão C#.

Para obter mais informações, consulte [árvores XML](functional-construction.md).

## <a name="see-also"></a>Confira também

- [Referência](reference.md)
- [LINQ to XML e DOM](linq-xml-vs-dom.md)
- [LINQ to XML vs. outras tecnologias XML](linq-xml-vs-xml-technologies.md)
- <xref:System.Xml.Linq>
