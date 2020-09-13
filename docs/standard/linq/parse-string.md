---
title: Como analisar um LINQ to XML de cadeia de caracteres
description: Você pode analisar uma cadeia de caracteres com XElement. Parse para criar uma árvore XML em C# e Visual Basic e pode criar uma árvore XML com literais XML no Visual Basic.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 81e5686c-9658-42d8-a7e3-b11be0a2c98b
ms.openlocfilehash: f4bd22acbf3b11d801c791cc591d882810450fd4
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551904"
---
# <a name="how-to-parse-a-string-linq-to-xml"></a>Como analisar uma cadeia de caracteres (LINQ to XML)

Este artigo mostra como analisar uma cadeia de caracteres para criar uma árvore XML em C# e em Visual Basic.

## <a name="example"></a>Exemplo

O código C# a seguir mostra como analisar uma cadeia de caracteres XML:

```csharp
XElement contacts = XElement.Parse(
    @"<Contacts>
        <Contact>
            <Name>Patrick Hines</Name>
            <Phone Type=""home"">206-555-0144</Phone>
            <Phone Type=""work"">425-555-0145</Phone>
            <Address>
            <Street1>123 Main St</Street1>
            <City>Mercer Island</City>
            <State>WA</State>
            <Postal>68042</Postal>
            </Address>
            <NetWorth>10</NetWorth>
        </Contact>
        <Contact>
            <Name>Gretchen Rivas</Name>
            <Phone Type=""mobile"">206-555-0163</Phone>
            <Address>
            <Street1>123 Main St</Street1>
            <City>Mercer Island</City>
            <State>WA</State>
            <Postal>68042</Postal>
            </Address>
            <NetWorth>11</NetWorth>
        </Contact>
    </Contacts>");
Console.WriteLine(contacts);
```

Você pode analisar uma cadeia de caracteres em Visual Basic de maneira semelhante. No entanto, é mais eficiente usar literais XML, como mostrado no código a seguir, porque os literais XML não sofrem com as mesmas penalidades de desempenho que a análise de XML de uma cadeia de caracteres.

Usando literais XML, você pode simplesmente copiar e colar o XML em seu programa Visual Basic.

> [!NOTE]
> Analisar texto ou carregar um documento XML de um arquivo de texto é menos eficiente do que a construção funcional. Se você estiver inicializando uma árvore XML do código, levará menos tempo do processador para usar a construção funcional do que analisar o texto.

```vb
Dim contacts as XElement = _
    <Contacts>
        <Contact>
            <Name>Patrick Hines</Name>
            <Phone Type="home">206-555-0144</Phone>
            <Phone Type="work">425-555-0145</Phone>
            <Address>
            <Street1>123 Main St</Street1>
            <City>Mercer Island</City>
            <State>WA</State>
            <Postal>68042</Postal>
            </Address>
            <NetWorth>10</NetWorth>
        </Contact>
        <Contact>
            <Name>Gretchen Rivas</Name>
            <Phone Type="mobile">206-555-0163</Phone>
            <Address>
            <Street1>123 Main St</Street1>
            <City>Mercer Island</City>
            <State>WA</State>
            <Postal>68042</Postal>
            </Address>
            <NetWorth>11</NetWorth>
        </Contact>
    </Contacts>
```

O `Contacts` nó raiz tem dois `Contact` nós. Para acessar alguns dados específicos em seu XML analisado, use o método [XElement. Elements ()](xref:System.Xml.Linq.XContainer.Elements) , que, nesse caso, retorna os elementos filho do `Contacts` nó raiz. O exemplo a seguir imprime o primeiro `Contact` nó no console:

```csharp
List<XElement> contactNodes = contacts.Elements("Contact").ToList();
Console.WriteLine(contactNodes[0]);
```

```vb
Dim contactNodes As List(Of XElement) = contacts.Elements("Contact").ToList()
Console.WriteLine(contactNodes(0))
```

## <a name="see-also"></a>Confira também

- [Como localizar um elemento com um atributo específico](find-element-specific-attribute.md)
