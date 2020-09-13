---
title: LINQ to XML e DOM
description: Há diferenças importantes entre LINQ to XML e DOM. O LINQ to XML dá suporte à construção funcional e a literais XML, o que mostra melhor a estrutura das árvores XML que elas criam.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 51c0e3d2-c047-4e6a-a423-d61a882400b7
ms.openlocfilehash: 905fe1b47361e2b96c79bc56cb831b3cb298e4de
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551975"
---
# <a name="linq-to-xml-vs-dom"></a>LINQ to XML e DOM

Este artigo descreve algumas das principais diferenças entre LINQ to XML e a API de programação XML predominante atual, o W3C Modelo de Objeto do Documento (DOM).

## <a name="new-ways-to-construct-xml-trees"></a>Novas maneiras de construir árvores XML

No W3C DOM, você cria uma árvore XML de baixo para cima; ou seja, você cria um documento, cria elementos e, em seguida, adiciona elementos ao documento.

Por exemplo, o exemplo a seguir usa uma maneira típica de criar uma árvore XML usando a implementação da Microsoft do DOM, <xref:System.Xml.XmlDocument> .

```csharp
XmlDocument doc = new XmlDocument();
XmlElement name = doc.CreateElement("Name");
name.InnerText = "Patrick Hines";
XmlElement phone1 = doc.CreateElement("Phone");
phone1.SetAttribute("Type", "Home");
phone1.InnerText = "206-555-0144";
XmlElement phone2 = doc.CreateElement("Phone");
phone2.SetAttribute("Type", "Work");
phone2.InnerText = "425-555-0145";
XmlElement street1 = doc.CreateElement("Street1");
street1.InnerText = "123 Main St";
XmlElement city = doc.CreateElement("City");
city.InnerText = "Mercer Island";
XmlElement state = doc.CreateElement("State");
state.InnerText = "WA";
XmlElement postal = doc.CreateElement("Postal");
postal.InnerText = "68042";
XmlElement address = doc.CreateElement("Address");
address.AppendChild(street1);
address.AppendChild(city);
address.AppendChild(state);
address.AppendChild(postal);
XmlElement contact = doc.CreateElement("Contact");
contact.AppendChild(name);
contact.AppendChild(phone1);
contact.AppendChild(phone2);
contact.AppendChild(address);
XmlElement contacts = doc.CreateElement("Contacts");
contacts.AppendChild(contact);
doc.AppendChild(contacts);
```

```vb
Dim doc As XmlDocument = New XmlDocument()
Dim name As XmlElement = doc.CreateElement("Name")
name.InnerText = "Patrick Hines"
Dim phone1 As XmlElement = doc.CreateElement("Phone")
phone1.SetAttribute("Type", "Home")
phone1.InnerText = "206-555-0144"
Dim phone2 As XmlElement = doc.CreateElement("Phone")
phone2.SetAttribute("Type", "Work")
phone2.InnerText = "425-555-0145"
Dim street1 As XmlElement = doc.CreateElement("Street1")
street1.InnerText = "123 Main St"
Dim city As XmlElement = doc.CreateElement("City")
city.InnerText = "Mercer Island"
Dim state As XmlElement = doc.CreateElement("State")
state.InnerText = "WA"
Dim postal As XmlElement = doc.CreateElement("Postal")
postal.InnerText = "68042"
Dim address As XmlElement = doc.CreateElement("Address")
address.AppendChild(street1)
address.AppendChild(city)
address.AppendChild(state)
address.AppendChild(postal)
Dim contact As XmlElement = doc.CreateElement("Contact")
contact.AppendChild(name)
contact.AppendChild(phone1)
contact.AppendChild(phone2)
contact.AppendChild(address)
Dim contacts As XmlElement = doc.CreateElement("Contacts")
contacts.AppendChild(contact)
doc.AppendChild(contacts)
Console.WriteLine(doc.OuterXml)
```

Esse estilo de codificação oculta a estrutura da árvore XML. O LINQ to XML também dá suporte a uma abordagem alternativa, *construção funcional*, que mostra melhor a estrutura. Essa abordagem pode ser feita com os <xref:System.Xml.Linq.XElement> <xref:System.Xml.Linq.XAttribute> construtores e. No Visual Basic, ele também pode ser feito com literais XML. Este exemplo demonstra a construção da mesma árvore XML usando a construção funcional:

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
Dim contacts = _
    <Contacts>
        <Contact>
            <Name>Patrick Hines</Name>
            <Phone Type="Home">206-555-0144</Phone>
            <Phone Type="Work">425-555-0145</Phone>
            <Address>
                <Street1>123 Main St</Street1>
                <City>Mercer Island</City>
                <State>WA</State>
                <Postal>68042</Postal>
            </Address>
        </Contact>
    </Contacts>
```

Observe que o recuo do código para construir a árvore XML mostra a estrutura do XML subjacente. A versão Visual Basic usa literais XML.

Para obter mais informações, consulte [árvores XML](functional-construction.md).

## <a name="work-directly-with-xml-elements"></a>Trabalhar diretamente com elementos XML

Quando você programa com XML, o foco principal é geralmente em elementos XML e talvez em atributos. No LINQ to XML, você pode trabalhar diretamente com elementos e atributos XML. Por exemplo, você pode fazer o seguinte:

- Criar elementos XML sem usar nenhum objeto de documento. Isso simplifica a programação quando você tem que trabalhar com partes de árvores XML.
- Carregue objetos `T:System.Xml.Linq.XElement` diretamente de um arquivo XML.
- Serialize objetos `T:System.Xml.Linq.XElement` para um arquivo ou fluxo.

Compare isso para o W3C DOM, no qual o documento XML é usado como um contêiner lógico para a árvore XML. No DOM, os nós XML, incluindo elementos e atributos, devem ser criados no contexto de um documento XML. Aqui está um fragmento de código para criar um elemento Name no DOM:

```csharp
XmlDocument doc = new XmlDocument();
XmlElement name = doc.CreateElement("Name");
name.InnerText = "Patrick Hines";
doc.AppendChild(name);
```

```vb
Dim doc As XmlDocument = New XmlDocument()
Dim name As XmlElement = doc.CreateElement("Name")
name.InnerText = "Patrick Hines"
doc.AppendChild(name)
```

Se você quiser usar um elemento em vários documentos, deverá importar os nós nos documentos. LINQ to XML evita essa camada de complexidade.

Ao usar LINQ to XML, você usará a classe <xref:System.Xml.Linq.XDocument> somente se você desejar adicionar um comentário ou uma instrução de processamento no nível raiz do documento.

## <a name="simplified-handling-of-names-and-namespaces"></a>Manipulação simplificada de nomes e namespaces

Tratar nomes, namespaces e prefixos de namespace é geralmente uma parte complexa da programação de XML. O LINQ to XML simplifica nomes e namespaces eliminando a necessidade de lidar com prefixos de namespace. Se quiser, você pode controlar prefixos de namespace. Mas se você decidir não controlar explicitamente os prefixos de namespace, LINQ to XML atribuirá prefixos de namespace durante a serialização, se eles forem necessários, ou serializarão usando namespaces padrão, se não forem. Se namespaces padrão forem usados, não haverá prefixos de namespace no documento resultante. Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

Outro problema com o DOM é que ele não permite que você altere o nome de um nó. Em vez disso, você precisa criar um novo nó e copiar todos os nós filhos para ele, perdendo a identidade do nó original. LINQ to XML evita esse problema permitindo que você defina a <xref:System.Xml.Linq.XName> propriedade em um nó.

## <a name="static-method-support-for-loading-xml"></a>Suporte de método estático para carregar XML

LINQ to XML permite carregar XML usando métodos estáticos, em vez de métodos de instância. Isso simplifica o carregamento e a análise. Para obter mais informações, consulte [como carregar XML de um arquivo](load-xml-file.md).

## <a name="removal-of-support-for-dtd-constructs"></a>Remoção de suporte para construções de DTD

LINQ to XML simplifica ainda mais a programação XML removendo o suporte para entidades e referências de entidade. O gerenciamento de entidades é complexo e raramente é usado. Remover o suporte aumenta o desempenho e simplifica a interface de programação. Quando uma árvore de LINQ to XML é populada, todas as entidades DTD são expandidas.

## <a name="support-for-fragments"></a>Suporte para fragmentos

LINQ to XML não fornece um equivalente para a `XmlDocumentFragment` classe. Em muitos casos, no entanto, o `XmlDocumentFragment` conceito pode ser tratado pelo resultado de uma consulta que é digitada a partir <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XNode> , ou <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XElement> .

## <a name="support-for-xpathnavigator"></a>Suporte para XPathNavigator

LINQ to XML fornece suporte para por <xref:System.Xml.XPath.XPathNavigator> meio de métodos de extensão no <xref:System.Xml.XPath?displayProperty=nameWithType> namespace. Para obter mais informações, consulte <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>.

## <a name="support-for-white-space-and-indentation"></a>Suporte para espaço em branco e recuo

LINQ to XML lida com o espaço em branco mais simples do que o DOM.

Um cenário comum é ler XML recuado, criar uma árvore XML na memória sem nenhum nó de texto de espaço em branco (ou seja, não preservar espaço em branco), executar algumas operações no XML e, em seguida, salvar o XML com recuo. Quando você serializa o XML com formatação, somente os espaços em branco significativos na árvore XML são preservados. Esse é o comportamento padrão para LINQ to XML.

Outro cenário comum é ler e modificar XML que já foi recuado intencionalmente. Você pode não querer modificar este recuo de nenhuma forma. No LINQ to XML, você pode fazer isso da seguinte:

- Preservando o espaço em branco quando você carrega ou analisa o XML.
- Desabilitar a formatação ao serializar o XML.

O LINQ to XML armazena espaço em branco como um <xref:System.Xml.Linq.XText> nó, em vez de ter um <xref:System.Xml.XmlNodeType.Whitespace> tipo de nó especializado, como o dom faz.

## <a name="support-for-annotations"></a>Suporte para anotações

LINQ to XML elementos dão suporte a um conjunto extensível de anotações. Isso é útil para acompanhar informações variadas sobre um elemento, como informações de esquema, informações sobre se o elemento está associado a uma interface do usuário ou qualquer outro tipo de informações específicas do aplicativo. Para obter mais informações, consulte [LINQ to XML anotações](linq-xml-annotations.md).

## <a name="support-for-schema-information"></a>Suporte para informações de esquema

LINQ to XML fornece suporte para validação XSD por meio de métodos de extensão no <xref:System.Xml.Schema?displayProperty=nameWithType> namespace. Você pode validar que uma árvore XML está em conformidade com XSD. Você pode preencher a árvore XML com o PSVI (post-schema-validation infoset). Para obter mais informações, consulte [como validar usando xsd](validate-xsd.md) e <xref:System.Xml.Schema.Extensions> .

## <a name="see-also"></a>Confira também

- [Visão geral de LINQ to XML](linq-xml-overview.md)
