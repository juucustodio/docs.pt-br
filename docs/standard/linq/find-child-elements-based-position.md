---
title: Como localizar elementos filho com base na LINQ to XML de posição
description: 'Saiba como localizar elementos de localização com base na posição do elemento. Três métodos são mostrados: um que usa XPathEvaluate, dois que usam LINQ to XML consulta.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: e35bb269-ec86-4c96-8321-12491a0eb2c3
ms.openlocfilehash: 889e3dbac3acf229fd49422285d650fc13792521
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557117"
---
# <a name="how-to-find-child-elements-based-on-position-linq-to-xml"></a>Como localizar elementos filho com base na posição (LINQ to XML)

Este artigo mostra como usar <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> o para localizar elementos com base na posição do elemento – por exemplo, para encontrar o segundo elemento ou o terceiro por meio do quinto. Ele também mostra duas maneiras de usar LINQ to XML consulta para fazer a mesma coisa.

Há duas abordagens para escrever essa LINQ to XML consulta de maneira lenta. Você pode usar os operadores de <xref:System.Linq.Enumerable.Skip%2A> e de <xref:System.Linq.Enumerable.Take%2A> , ou você pode usar a sobrecarga de <xref:System.Linq.Enumerable.Where%2A> que usa um índice. Quando você usa a sobrecarga de <xref:System.Linq.Enumerable.Where%2A> , você usa uma expressão lambda que leva dois argumentos. O exemplo a seguir mostra os dois métodos de selecione a posição de functionamento base.

## <a name="example-find-the-second-through-the-fourth-test-elements"></a>Exemplo: Localize o segundo por meio dos quarto `Test` elementos

Este exemplo localiza o segundo por meio do quarto `Test` elemento no [arquivo XML de exemplo: configuração de teste](sample-xml-file-test-configuration.md). O resultado é uma coleção de elementos.

A expressão XPath é `Test[position() >= 2 and position() <= 4]`.

```csharp
XElement testCfg = XElement.Load("TestConfig.xml");

// LINQ to XML query
IEnumerable<XElement> list1 =
    testCfg
    .Elements("Test")
    .Skip(1)
    .Take(3);

// LINQ to XML query
IEnumerable<XElement> list2 =
    testCfg
    .Elements("Test")
    .Where((el, idx) => idx >= 1 && idx <= 3);

// XPath expression
IEnumerable<XElement> list3 =
  testCfg.XPathSelectElements("Test[position() >= 2 and position() <= 4]");

if (list1.Count() == list2.Count() &&
    list1.Count() == list3.Count() &&
    list1.Intersect(list2).Count() == list1.Count() &&
    list1.Intersect(list3).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim testCfg As XElement = XElement.Load("TestConfig.xml")

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = _
    testCfg.Elements("Test").Skip(1).Take(3)

'LINQ to XML query
Dim list2 As IEnumerable(Of XElement) = _
    testCfg.Elements("Test"). _
    Where(Function(ByVal el, ByVal idx) idx >= 1 And idx <= 3)

' XPath expression
Dim list3 As IEnumerable(Of XElement) = _
    testCfg.XPathSelectElements("Test[position() >= 2 and position() <= 4]")

If list1.Count() = list2.Count() And _
       list1.Count() = list3.Count() And _
       list1.Intersect(list2).Count() = list1.Count() And _
       list1.Intersect(list3).Count() = list1.Count() Then

    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If

For Each el As XElement In list1
    Console.WriteLine(el)
Next
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
<Test TestId="0002" TestType="CMD">
  <Name>Find succeeding characters</Name>
  <CommandLine>Examp2.EXE</CommandLine>
  <Input>abc</Input>
  <Output>def</Output>
</Test>
<Test TestId="0003" TestType="GUI">
  <Name>Convert multiple numbers to strings</Name>
  <CommandLine>Examp2.EXE /Verbose</CommandLine>
  <Input>123</Input>
  <Output>One Two Three</Output>
</Test>
<Test TestId="0004" TestType="GUI">
  <Name>Find correlated key</Name>
  <CommandLine>Examp3.EXE</CommandLine>
  <Input>a1</Input>
  <Output>b1</Output>
</Test>
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](./comparison-xpath-linq-xml.md)
