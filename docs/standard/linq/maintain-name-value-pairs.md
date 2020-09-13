---
title: Manter pares de nome-valor-LINQ to XML
description: Saiba como usar os métodos de LINQ to XML para manter um conjunto de pares de nome-valor.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 7b04b0f1-af64-42eb-8737-83f8861b5915
ms.openlocfilehash: 681df91d42f8bdb403dcf6f735104301c4a0c9ba
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551964"
---
# <a name="maintain-name-value-pairs-linq-to-xml"></a>Manter pares de nome-valor (LINQ to XML)

Muitos aplicativos precisam manter as informações que são mais bem mantidas como pares de nome-valor. Essas informações podem ser informações de configuração ou configurações globais. LINQ to XML contém métodos que facilitam a manutenção de um conjunto de pares de nome-valor. É possível manter informações como atributos ou como um conjunto de elementos filho.

Uma das diferenças entre manter as informações como atributos ou como elementos filho é que os atributos possuem a restrição de que pode existir apenas um atributo com um nome específico para um elemento. Essa limitação não se aplica a elementos filho.

## <a name="setattributevalue-and-setelementvalue"></a>SetAttributeValue e SetElementValue

Os dois métodos que facilitam a manutenção de pares de nome-valor são <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> e <xref:System.Xml.Linq.XElement.SetElementValue%2A> . Esses dois métodos possuem semântica semelhante.

<xref:System.Xml.Linq.XElement.SetAttributeValue%2A> pode adicionar, modificar e remover atributos de um elemento.

- Se você chamar <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> com um nome de um atributo que não existe, o método criará um novo atributo e o adicionará ao elemento especificado.
- Ao designar <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> com o nome de um atributo existente e algum conteúdo especificado, o conteúdo do atributo é substituído pelo conteúdo especificado.
- Se você chamar <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> com um nome de um atributo existente e especificar `null` para o conteúdo, o atributo será removido de seu pai.

<xref:System.Xml.Linq.XElement.SetElementValue%2A> pode adicionar, modificar e remover elementos filho de um elemento.

- Se você chamar <xref:System.Xml.Linq.XElement.SetElementValue%2A> com um nome de um elemento filho que não existe, o método criará um novo elemento e o adicionará ao elemento especificado.
- Ao designar <xref:System.Xml.Linq.XElement.SetElementValue%2A> com o nome de um elemento existente e algum conteúdo especificado, o conteúdo do elemento é substituído pelo conteúdo especificado.
- Se você chamar <xref:System.Xml.Linq.XElement.SetElementValue%2A> com um nome de um elemento existente e especificar `null` para o conteúdo, o elemento será removido de seu pai.

## <a name="example-use-setattributevalue-to-create-and-maintain-a-list-of-name-value-pairs"></a>Exemplo: use `SetAttributeValue` para criar e manter uma lista de pares de nome-valor

O exemplo a seguir cria um elemento sem atributos. Em seguida, ele usa o <xref:System.Xml.Linq.XElement.SetAttributeValue%2A> método para criar e manter uma lista de pares de nome-valor.

```csharp
// Create an element with no content.
XElement root = new XElement("Root");

// Add a number of name-value pairs as attributes.
root.SetAttributeValue("Top", 22);
root.SetAttributeValue("Left", 20);
root.SetAttributeValue("Bottom", 122);
root.SetAttributeValue("Right", 300);
root.SetAttributeValue("DefaultColor", "Color.Red");
Console.WriteLine(root);

// Replace the value of Top.
root.SetAttributeValue("Top", 10);
Console.WriteLine(root);

// Remove DefaultColor.
root.SetAttributeValue("DefaultColor", null);
Console.WriteLine(root);
```

```vb
' Create an element with no content.
Dim root As XElement = <Root/>

' Add a number of name-value pairs as attributes.
root.SetAttributeValue("Top", 22)
root.SetAttributeValue("Left", 20)
root.SetAttributeValue("Bottom", 122)
root.SetAttributeValue("Right", 300)
root.SetAttributeValue("DefaultColor", "Color.Red")
Console.WriteLine(root)

' Replace the value of Top.
root.SetAttributeValue("Top", 10)
Console.WriteLine(root)

' Remove DefaultColor.
root.SetAttributeValue("DefaultColor", Nothing)
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root Top="22" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />
<Root Top="10" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />
<Root Top="10" Left="20" Bottom="122" Right="300" />
```

## <a name="example-use-setelementvalue-to-create-and-maintain-a-list-of-name-value-pairs"></a>Exemplo: use `SetElementValue` para criar e manter uma lista de pares de nome-valor

O exemplo a seguir cria um elemento sem elementos filho. Em seguida, ele usa o <xref:System.Xml.Linq.XElement.SetElementValue%2A> método para criar e manter uma lista de pares de nome-valor.

```csharp
// Create an element with no content.
XElement root = new XElement("Root");

// Add a number of name-value pairs as elements.
root.SetElementValue("Top", 22);
root.SetElementValue("Left", 20);
root.SetElementValue("Bottom", 122);
root.SetElementValue("Right", 300);
root.SetElementValue("DefaultColor", "Color.Red");
Console.WriteLine(root);
Console.WriteLine("----");

// Replace the value of Top.
root.SetElementValue("Top", 10);
Console.WriteLine(root);
Console.WriteLine("----");

// Remove DefaultColor.
root.SetElementValue("DefaultColor", null);
Console.WriteLine(root);
```

```vb
' Create an element with no content.
Dim root As XElement = <Root/>

' Add a number of name-value pairs as elements.
root.SetElementValue("Top", 22)
root.SetElementValue("Left", 20)
root.SetElementValue("Bottom", 122)
root.SetElementValue("Right", 300)
root.SetElementValue("DefaultColor", "Color.Red")
Console.WriteLine(root)
Console.WriteLine("----")

' Replace the value of Top.
root.SetElementValue("Top", 10)
Console.WriteLine(root)
Console.WriteLine("----")

' Remove DefaultColor.
root.SetElementValue("DefaultColor", Nothing)
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Top>22</Top>
  <Left>20</Left>
  <Bottom>122</Bottom>
  <Right>300</Right>
  <DefaultColor>Color.Red</DefaultColor>
</Root>
----
<Root>
  <Top>10</Top>
  <Left>20</Left>
  <Bottom>122</Bottom>
  <Right>300</Right>
  <DefaultColor>Color.Red</DefaultColor>
</Root>
----
<Root>
  <Top>10</Top>
  <Left>20</Left>
  <Bottom>122</Bottom>
  <Right>300</Right>
</Root>
```

## <a name="see-also"></a>Confira também

- <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>
- <xref:System.Xml.Linq.XElement.SetElementValue%2A>
