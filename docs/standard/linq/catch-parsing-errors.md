---
title: Como detectar erros de análise-LINQ to XML
description: Uma exceção pode ocorrer em seu programa C# ou Visual Basic se tentar analisar um XML inválido com um método como XElement. Parse. Você pode escrever o programa para detectar e responder a essas exceções.
ms.date: 7/20/2015
dev_langs:
- csharp
- vb
ms.assetid: bfb612d4-5605-48ef-8c93-915cf9d5dcfb
ms.openlocfilehash: f7679bd5a0726c669eb47ad6ad66e0f64259264b
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551886"
---
# <a name="how-to-catch-parsing-errors-linq-to-xml"></a>Como capturar erros de análise (LINQ to XML)

Este artigo mostra como detectar XML mal formado ou inválido em C# ou Visual Basic.

O LINQ to XML é implementado usando <xref:System.Xml.XmlReader> . Se XML mal formado ou inválido for passado para LINQ to XML, a <xref:System.Xml.XmlReader> classe subjacente gerará uma exceção. Os vários métodos que analisam XML, como <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType> , não capturam a exceção; a exceção pode ser detectada pelo seu aplicativo.

## <a name="example-parse-invalid-xml"></a>Exemplo: analisar XML inválido

O código a seguir tenta analisar um XML inválido.

```csharp
try {
    XElement contacts = XElement.Parse(
        @"<Contacts>
            <Contact>
                <Name>Jim Wilson</Name>
            </Contact>
          </Contcts>");

    Console.WriteLine(contacts);
}
catch (System.Xml.XmlException e)
{
    Console.WriteLine(e.Message);
}
```

```vb
Try
    Dim contacts As XElement = XElement.Parse("<Contacts>" & vbCrLf & _
        "    <Contact>" & vbCrLf & _
        "        <Name>Jim Wilson</Name>" & vbCrLf & _
        "    </Contact>" & vbCrLf & _
        "</Contcts>")

    Console.WriteLine(contacts)
Catch e As System.Xml.XmlException
    Console.WriteLine(e.Message)
End Try
```

Devido à marca de fim inválida `</Contcts>` , o exemplo gera a seguinte exceção:

```output
The 'Contacts' start tag on line 1 doesn't match the end tag of 'Contcts'. Line 5, position 13.
```

Para obter informações sobre as exceções que <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType> os <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType> métodos,, <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType> e <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType> geram, consulte a <xref:System.Xml.XmlReader> documentação.

## <a name="see-also"></a>Confira também

- [Como analisar uma cadeia de caracteres](parse-string.md)
