---
title: Como executar transformações de streaming de texto em XML em C#-LINQ to XML
description: Você pode usar um método de extensão que libera uma linha por vez para transmitir um arquivo de texto para processamento. Essa técnica reduz os requisitos de memória em comparação com as técnicas que carregam todo o arquivo e depois o processam.
ms.date: 07/20/2015
dev_langs:
- csharp
ms.assetid: 9b3bd941-d0ff-4f2d-ae41-7c3b81d8fae6
ms.openlocfilehash: 8e0d710d7cbc6de8cc60721c211376a82b6c29fc
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552308"
---
# <a name="how-to-perform-streaming-transformations-of-text-to-xml-in-c-linq-to-xml"></a>Como executar transformações de streaming de texto em XML em C# (LINQ to XML)

Você pode usar um método de extensão que libera uma linha por vez para transmitir um arquivo de texto para processamento. Essa técnica reduz os requisitos de memória em comparação com as técnicas que carregam todo o arquivo e depois o processam.

O método de extensão pode fornecer a linha usando a `yield return` construção. Uma consulta LINQ pode processar o fluxo de forma retardada de modo lento. Se você usar <xref:System.Xml.Linq.XStreamingElement> o para transmitir a saída, poderá criar uma transformação do arquivo de texto para XML que usa uma quantidade mínima de memória, independentemente do tamanho do arquivo de texto de origem.

> [!NOTE]
> A técnica é melhor aplicada em situações nas quais você pode processar todo o arquivo uma vez, levando em ordem as linhas do documento de origem. O processamento do arquivo mais de uma vez ou a classificação antes do processamento reduz os benefícios de desempenho de uma técnica de streaming.

## <a name="example-use-an-extension-method-to-stream-text"></a>Exemplo de uso de um método de extensão para transmitir texto

O exemplo usa o seguinte arquivo de texto, People.txt, como sua fonte:

```text
#This is a comment
1,Tai,Yee,Writer
2,Nikolay,Grachev,Programmer
3,David,Wright,Inventor
```

No código para o exemplo, o método de extensão `Lines` fornece o texto uma linha por vez:

```csharp
public static class StreamReaderSequence
{
    public static IEnumerable<string> Lines(this StreamReader source)
    {
        if (source == null)
            throw new ArgumentNullException(nameof(source));

        string line;
        while ((line = source.ReadLine()) != null)
        {
            yield return line;
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        var sr = new StreamReader("People.txt");
        var xmlTree = new XStreamingElement("Root",
            from line in sr.Lines()
            let items = line.Split(',')
            where !line.StartsWith("#")
            select new XElement("Person",
                       new XAttribute("ID", items[0]),
                       new XElement("First", items[1]),
                       new XElement("Last", items[2]),
                       new XElement("Occupation", items[3])
                   )
        );
        Console.WriteLine(xmlTree);
        sr.Close();
    }
}
```

O exemplo produz a seguinte saída:

```xml
<Root>
  <Person ID="1">
    <First>Tai</First>
    <Last>Yee</Last>
    <Occupation>Writer</Occupation>
  </Person>
  <Person ID="2">
    <First>Nikolay</First>
    <Last>Grachev</Last>
    <Occupation>Programmer</Occupation>
  </Person>
  <Person ID="3">
    <First>David</First>
    <Last>Wright</Last>
    <Occupation>Inventor</Occupation>
  </Person>
</Root>
```

## <a name="see-also"></a>Confira também

- <xref:System.Xml.Linq.XStreamingElement>
