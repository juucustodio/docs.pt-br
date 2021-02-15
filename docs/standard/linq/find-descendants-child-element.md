---
title: Como localizar descendentes de um elemento filho-LINQ to XML
description: 'Saiba como localizar descendentes de um elemento filho ou uma sequência de elementos filho. Dois métodos são mostrados: um usa XPathEvaluate, o outro usa LINQ to XML consulta.'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 505b7512-bb8b-4f85-abbf-491f039c961e
ms.openlocfilehash: 2ac023ddc797f27f5f00eaf86ff6357096f333c8
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90559311"
---
# <a name="how-to-find-descendants-of-a-child-element-linq-to-xml"></a>Como localizar descendentes de um elemento filho (LINQ to XML)

Este artigo mostra como usar <xref:System.Xml.XPath.Extensions.XPathEvaluate%2A> o para localizar os elementos descendentes de uma sequência de elementos filho e como usar LINQ to XML consulta para localizar os mesmos elementos.

## <a name="example-find-all-the-text-descendant-elements-of-all-the-paragraph-elements"></a>Exemplo: localizar todos os `Text` elementos descendentes de todos os `Paragraph` elementos

Este exemplo extrai o texto de uma representação XML de um documento simples de processamento de texto. Primeiro, ele seleciona todos os `Paragraph` elementos, ignorando o `Comment` elemento e seleciona todos os `Text` elementos descendentes de cada `Paragraph` elemento. Ele realiza essa tarefa de duas maneiras: com <xref:System.Xml.XPath.Extensions.XPathEvaluate%2A> e com LINQ to XML consulta. Em seguida, ele compara os resultados e os encontra idênticos.

A expressão XPath é  `./Paragraph//Text/text()` .

```csharp
XElement root = XElement.Parse(
@"<Root>
  <Paragraph>
    <Text>This is the start of</Text>
  </Paragraph>
  <Comment>
    <Text>This comment isn't part of the paragraph text.</Text>
  </Comment>
  <Paragraph>
    <Annotation Emphasis='true'>
      <Text> a sentence.</Text>
    </Annotation>
  </Paragraph>
  <Paragraph>
    <Text>  This is the second sentence.</Text>
  </Paragraph>
</Root>");

// LINQ to XML query
string str1 =
    root
    .Elements("Paragraph")
    .Descendants("Text")
    .Select(s => s.Value)
    .Aggregate(
        new StringBuilder(),
        (s, i) => s.Append(i),
        s => s.ToString()
    );

// XPath expression
string str2 =
    ((IEnumerable)root.XPathEvaluate("./Paragraph//Text/text()"))
    .Cast<XText>()
    .Select(s => s.Value)
    .Aggregate(
        new StringBuilder(),
        (s, i) => s.Append(i),
        s => s.ToString()
    );

if (str1 == str2)
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
Console.WriteLine(str2);
```

```vb
Dim root As XElement = _
    <Root>
        <Paragraph>
            <Text>This is the start of</Text>
        </Paragraph>
        <Comment>
            <Text>This comment isn't part of the paragraph text.</Text>
        </Comment>
        <Paragraph>
            <Annotation Emphasis='true'>
                <Text> a sentence.</Text>
            </Annotation>
        </Paragraph>
        <Paragraph>
            <Text>This is the second sentence.</Text>
        </Paragraph>
    </Root>

' LINQ to XML query
Dim str1 As String = _
    root.<Paragraph>...<Text>.Select(Function(ByVal s) s.Value). _
    Aggregate( _
        New StringBuilder(), _
        Function(ByVal s, ByVal i) s.Append(i), _
        Function(ByVal s) s.ToString())

' XPath expression
Dim str2 As String = DirectCast(root.XPathEvaluate("./Paragraph//Text/text()"), IEnumerable) _
    .Cast(Of XText)().Select(Function(ByVal s) s.Value) _
    .Aggregate( _
        New StringBuilder(), _
        Function(ByVal s, ByVal i) s.Append(i), _
        Function(ByVal s) s.ToString())

If str1 = str2 Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
Console.WriteLine(str2)
```

Esse exemplo gera a saída a seguir:

```output
Results are identical
This is the start of a sentence.  This is the second sentence.
```

## <a name="see-also"></a>Confira também

- [LINQ to XML para usuários do XPath (Visual Basic)](./comparison-xpath-linq-xml.md)
