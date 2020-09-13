---
title: Recuperar os parágrafos e seus estilos-LINQ to XML
description: Saiba como recuperar nós de parágrafo e seus estilos de um documento do WordprocessingML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: c2f767f8-57b1-4b4b-af04-89ffb1f7067d
ms.openlocfilehash: 43c6173441dda841236a4397e28d0bb2c7c8d003
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552064"
---
# <a name="retrieve-the-paragraphs-and-their-styles-linq-to-xml"></a>Recuperar os parágrafos e seus estilos (LINQ to XML)

Nesse exemplo, nós escrevemos uma consulta que recupera os nós de parágrafo de um documento de WordprocessingML. Também identifica o estilo de cada parágrafo.

Essa consulta se baseia na consulta no exemplo anterior, [localize o estilo de parágrafo padrão](find-default-paragraph-style.md), que recupera o estilo padrão da lista de estilos. Essas informações são necessárias para que a consulta possa identificar o estilo dos parágrafos que não têm um estilo explicitamente definido. Os estilos de parágrafo são definidos por meio do `w:pPr` elemento; se um parágrafo não contiver esse elemento, ele será formatado com o estilo padrão.

Este artigo explica a significância de algumas partes da consulta e, em seguida, mostra a consulta como parte de um exemplo funcional completo.

## <a name="example-retrieve-all-the-paragraphs-in-a-document-and-the-paragraph-styles"></a>Exemplo: recuperar todos os parágrafos em um documento e os estilos de parágrafo

O código a seguir é uma consulta para recuperar todos os parágrafos em um documento e seus estilos:

```csharp
xDoc.Root.Element(w + "body").Descendants(w + "p")
```

```vb
xDoc.Root.<w:body>...<w:p>
```

Essa expressão é semelhante à origem da consulta no exemplo anterior, [localizar o estilo de parágrafo padrão](find-default-paragraph-style.md). A principal diferença é que usa o eixo de <xref:System.Xml.Linq.XContainer.Descendants%2A> em vez do eixo de <xref:System.Xml.Linq.XContainer.Elements%2A> . A consulta usa o <xref:System.Xml.Linq.XContainer.Descendants%2A> eixo porque, em documentos que têm seções, os parágrafos não serão os filhos diretos do elemento body; em vez disso, os parágrafos serão dois níveis abaixo na hierarquia. Usando o <xref:System.Xml.Linq.XContainer.Descendants%2A> eixo, o código funcionará se o documento usar ou não seções.

## <a name="example-use-a-let-clause-to-determine-the-element-that-contains-the-style-node"></a>Exemplo: Use uma `let` cláusula para determinar o elemento que contém o nó de estilo

A consulta a seguir usa uma `let` cláusula para determinar o elemento que contém o nó de estilo:

```csharp
let styleNode = para.Elements(w + "pPr").Elements(w + "pStyle").FirstOrDefault()
```

 ```vb
Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault()
```

A `let` cláusula ( `Let` na versão Visual Basic) primeiro usa o <xref:System.Xml.Linq.XContainer.Elements%2A> eixo para localizar todos os elementos chamados `pPr` , em seguida, usa o <xref:System.Xml.Linq.Extensions.Elements%2A> método de extensão para localizar todos os elementos filho chamados `pStyle` e, por fim, usa o <xref:System.Linq.Enumerable.FirstOrDefault%2A> operador de consulta padrão para converter a coleção em um singleton. Se a coleção estiver vazia, `styleNode` será definida como `null` ( `Nothing` na versão Visual Basic). Este é um idioma útil para procurar o nó descendente de `pStyle` . Observe que, se o `pPr` nó filho não existir, o código não falhará lançando uma exceção; em vez disso, `styleNode` será definido como `null` ( `Nothing` ), que é o comportamento desejado dessa `let` `Let` cláusula ().

Se não houver nenhum elemento, `styleNode` será definido como `null` ( `Nothing` ).

A consulta em uma coleção de um tipo anônimo com dois membros, `StyleName` e `ParagraphNode`.

## <a name="example-retrieve-the-paragraph-nodes-from-a-wordprocessingml-document"></a>Exemplo: recuperar os nós de parágrafo de um documento do WordprocessingML

Este exemplo processa um documento do WordprocessingML, recuperando os nós de parágrafo. Também identifica o estilo de cada parágrafo. Este exemplo cria nos exemplos anteriores neste tutorial. A nova consulta é chamada nos comentários no código a seguir.

As instruções para criar o documento de origem para este exemplo estão em [criar o documento Office Open XML de origem](create-source-office-open-xml-document.md).

Este exemplo usa as classes encontradas no assembly WindowsBase. Ele usa tipos no namespace <xref:System.IO.Packaging?displayProperty=nameWithType>.

```csharp
const string fileName = "SampleDoc.docx";

const string documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";
const string stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";
const string wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main";
XNamespace w = wordmlNamespace;

XDocument xDoc = null;
XDocument styleDoc = null;

using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))
{
    PackageRelationship docPackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();
    if (docPackageRelationship != null)
    {
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative), docPackageRelationship.TargetUri);
        PackagePart documentPart = wdPackage.GetPart(documentUri);

        //  Load the document XML in the part into an XDocument instance.
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));

        //  Find the styles part. There will only be one.
        PackageRelationship styleRelation = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();
        if (styleRelation != null)
        {
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);
            PackagePart stylePart = wdPackage.GetPart(styleUri);

            //  Load the style XML in the part into an XDocument instance.
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));
        }
    }
}

string defaultStyle =
    (string)(
        from style in styleDoc.Root.Elements(w + "style")
        where (string)style.Attribute(w + "type") == "paragraph"&&
              (string)style.Attribute(w + "default") == "1"
              select style
    ).First().Attribute(w + "styleId");

// Following is the new query that finds all paragraphs in the
// document and their styles.
var paragraphs =
    from para in xDoc
                 .Root
                 .Element(w + "body")
                 .Descendants(w + "p")
    let styleNode = para
                    .Elements(w + "pPr")
                    .Elements(w + "pStyle")
                    .FirstOrDefault()
    select new
    {
        ParagraphNode = para,
        StyleName = styleNode != null ?
            (string)styleNode.Attribute(w + "val") :
            defaultStyle
    };

foreach (var p in paragraphs)
    Console.WriteLine("StyleName:{0}", p.StyleName);
```

```vb
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">

Module Module1
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, ByVal defaultStyle As String) As String
        If (styleNode Is Nothing) Then
            Return defaultStyle
        Else
            Return styleNode.@w:val
        End If
    End Function

    Sub Main()
        Dim fileName = "SampleDoc.docx"

        Dim documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"
        Dim stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"
        Dim wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main"

        Dim xDoc As XDocument = Nothing
        Dim styleDoc As XDocument = Nothing
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)
            Dim docPackageRelationship As PackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()
            If (docPackageRelationship IsNot Nothing) Then
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), docPackageRelationship.TargetUri)
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)

                '  Load the document XML in the part into an XDocument instance.
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))

                '  Find the styles part. There will only be one.
                Dim styleRelation As PackageRelationship = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()
                If (styleRelation IsNot Nothing) Then
                    Dim styleUri As Uri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)
                    Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)

                    '  Load the style XML in the part into an XDocument instance.
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()))
                End If
            End If
        End Using

        Dim defaultStyle As String = _
            ( _
                From style In styleDoc.Root.<w:style> _
                Where style.@w:type = "paragraph" And _
                      style.@w:default = "1" _
                Select style _
            ).First().@w:styleId

        ' Following is the new query that finds all paragraphs in the
        ' document and their styles.
        Dim paragraphs = _
            From para In xDoc.Root.<w:body>...<w:p> _
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault() _
        Select New With { _
            .ParagraphNode = para, _
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _
        }

        For Each p In paragraphs
            Console.WriteLine("StyleName:{0}", p.StyleName)
        Next

    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
StyleName:Heading1
StyleName:Normal
StyleName:Normal
StyleName:Normal
StyleName:Code
StyleName:Code
StyleName:Code
StyleName:Code
StyleName:Code
StyleName:Code
StyleName:Code
StyleName:Normal
StyleName:Normal
StyleName:Normal
StyleName:Code
```

O próximo artigo deste tutorial mostra como criar uma consulta para recuperar o texto de parágrafos:

- [Recuperar o texto dos parágrafos](retrieve-text-paragraphs.md)

## <a name="see-also"></a>Confira também

- [Tutorial: manipular conteúdo em um documento do WordprocessingML](xml-shape-wordprocessingml-documents.md)
