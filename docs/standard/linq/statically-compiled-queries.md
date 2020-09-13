---
title: Consultas compiladas estaticamente-LINQ to XML
description: Saiba como LINQ to XML consultas obtenha uma vantagem de desempenho sobre o XMLDocument, sendo compilado estaticamente.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 3bf558fe-0705-479d-86d4-00188f5fcf9c
ms.openlocfilehash: 53dd47247eae8802dcf8187d0e82eb1c8bead9f9
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551998"
---
# <a name="statically-compiled-queries-linq-to-xml"></a>Consultas compiladas estaticamente (LINQ to XML)

Uma das vantagens de desempenho mais importantes do LINQ to XML, em comparação com o <xref:System.Xml.XmlDocument> , é que as consultas no LINQ to XML são compiladas estaticamente, enquanto as consultas XPath devem ser interpretadas em tempo de execução. Esse recurso é criado em LINQ to XML, de modo que você não precisa executar etapas adicionais para aproveitar isso, mas é útil entender a distinção ao escolher entre as duas tecnologias. Este artigo explica a diferença.

## <a name="statically-compiled-queries-vs-xpath"></a>Consultas compiladas estaticamente versus XPath

O exemplo a seguir mostra como obter os elementos descendentes com um nome especificado e, com um atributo com um valor especificado. A expressão XPath equivalente é `//Address[@Type='Shipping']` .

```csharp
XDocument po = XDocument.Load("PurchaseOrders.xml");

IEnumerable<XElement> list1 =
    from el in po.Descendants("Address")
    where (string)el.Attribute("Type") == "Shipping"
    select el;

foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim po = XDocument.Load("PurchaseOrders.xml")

Dim list1 = From el In po.Descendants("Address")
            Where el.@Type = "Shipping"

For Each el In list1
    Console.WriteLine(el)
Next
```

A expressão de consulta neste exemplo é reescrita pelo compilador para sintaxe de consulta baseada em método. O exemplo a seguir, que é escrito na sintaxe da consulta com base em método, gerenciar os mesmos resultados que anterior:

```csharp
XDocument po = XDocument.Load("PurchaseOrders.xml");

IEnumerable<XElement> list1 =
    po
    .Descendants("Address")
    .Where(el => (string)el.Attribute("Type") == "Shipping");

foreach (XElement el in list1)
    Console.WriteLine(el);
```

 ```vb
Dim po = XDocument.Load("PurchaseOrders.xml")

Dim list1 As IEnumerable(Of XElement) = po.Descendants("Address").Where(Function(el) el.@Type = "Shipping")

For Each el In list1
    Console.WriteLine(el)
Next
```

O método de <xref:System.Linq.Enumerable.Where%2A> é um método de extensão. Para obter mais informações, consulte [métodos de extensão (guia de programação C#)](../../csharp/programming-guide/classes-and-structs/extension-methods.md). Porque <xref:System.Linq.Enumerable.Where%2A> é um método de extensão, a consulta anterior é criada como se ele foi gravado como segue:

```csharp
XDocument po = XDocument.Load("PurchaseOrders.xml");

IEnumerable<XElement> list1 =
    System.Linq.Enumerable.Where(
        po.Descendants("Address"),
        el => (string)el.Attribute("Type") == "Shipping");

foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim po = XDocument.Load("PurchaseOrders.xml")

Dim list1 = Enumerable.Where(po.Descendants("Address"), Function(el) el.@Type = "Shipping")

For Each el In list1
    Console.WriteLine(el)
Next
```

Este exemplo gerencia exatamente os mesmos resultados que os dois exemplos anteriores. Isso ilustra o fato de que as consultas são compiladas efetivamente estaticamente associados em chamadas de método. Isso, combinado com a semântica de execução adiada de iteradores, melhora o desempenho. Para obter mais informações sobre a semântica de execução adiada de iteradores, consulte [execução retardada e avaliação lenta](deferred-execution-lazy-evaluation.md).

> [!NOTE]
> Esses exemplos são representante de código que o compilador pode escrever. A implementação real pode ser ligeiramente diferente desses exemplos, mas o desempenho será o mesmo que, ou semelhante, a esses exemplos.

## <a name="executing-xpath-expressions-with-xmldocument"></a>Executando expressões XPath com XmlDocument

O exemplo a seguir usa <xref:System.Xml.XmlDocument> para executar os mesmos resultados que os exemplos anteriores:

```csharp
XmlReader reader = XmlReader.Create("PurchaseOrders.xml");
XmlDocument doc = new XmlDocument();
doc.Load(reader);
XmlNodeList nl = doc.SelectNodes(".//Address[@Type='Shipping']");
foreach (XmlNode n in nl)
    Console.WriteLine(n.OuterXml);
reader.Close();
```

```vb
Dim reader = Xml.XmlReader.Create("PurchaseOrders.xml")
Dim doc As New Xml.XmlDocument()
doc.Load(reader)
Dim nl As Xml.XmlNodeList = doc.SelectNodes(".//Address[@Type='Shipping']")
For Each n As Xml.XmlNode In nl
    Console.WriteLine(n.OuterXml)
Next
reader.Close()
```

Essa consulta retorna a mesma saída que os exemplos que usam LINQ to XML; a única diferença é que LINQ to XML recua o XML impresso, enquanto <xref:System.Xml.XmlDocument> não.

No entanto, a <xref:System.Xml.XmlDocument> abordagem geralmente não é executada, bem como LINQ to XML, porque o <xref:System.Xml.XmlNode.SelectNodes%2A> método deve fazer o seguinte sempre que for chamado:

- Analise a cadeia de caracteres que contém a expressão XPath, dividindo a cadeia de caracteres em tokens.
- Valide os tokens para certificar-se de que a expressão XPath é válida.
- Traduza a expressão em uma árvore de expressão interna.
- Itere os nós, selecionando adequadamente os nós para o conjunto de resultados com base na avaliação da expressão.

Este é significativamente mais do que o trabalho feito pela consulta correspondente LINQ to XML. A diferença desempenho específico variam para tipos diferentes de consultas, mas em geral LINQ to XML consultas menos trabalho e, portanto, executam melhor do que as expressões XPath de avaliação usando <xref:System.Xml.XmlDocument>.
