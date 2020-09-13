---
title: Exemplo que gera partes do documento XML aberto do Office-LINQ to XML
description: Saiba como abrir um documento XML aberto do Office e acessar suas partes.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 6cd37055-89b4-42e8-bf27-5a29717e35f3
ms.openlocfilehash: 68ecdc573eaafd706c3082c736243874cb8dcc30
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551850"
---
# <a name="example-that-outputs-office-open-xml-document-parts-linq-to-xml"></a>Exemplo que gera as partes do documento XML aberto do Office (LINQ to XML)

Este artigo mostra como abrir um documento XML aberto do Office e acessar suas partes.

## <a name="example-print-the-document-and-style-parts-of-an-office-open-xml-document"></a>Exemplo: imprimir as partes de documento e estilo de um documento XML aberto do Office

O exemplo a seguir abre um documento XML aberto do Office e imprime as partes de documento e estilos.

Este exemplo usa classes do assembly WindowsBase e tipos do <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.

```csharp
const string fileName = "SampleDoc.docx";

const string documentRelationshipType =
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";
const string stylesRelationshipType =
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";
const string wordmlNamespace =
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";
XNamespace w = wordmlNamespace;

using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))
{
    PackageRelationship docPackageRelationship =
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();
    if (docPackageRelationship != null)
    {
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),
          docPackageRelationship.TargetUri);
        PackagePart documentPart = wdPackage.GetPart(documentUri);

        //  Load the document XML in the part into an XDocument instance.
        XDocument xdoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));

        Console.WriteLine("TargetUri:{0}", docPackageRelationship.TargetUri);
        Console.WriteLine("==================================================================");
        Console.WriteLine(xdoc.Root);
        Console.WriteLine();

        //  Find the styles part. There will only be one.
        PackageRelationship styleRelation =
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();
        if (styleRelation != null)
        {
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);
            PackagePart stylePart = wdPackage.GetPart(styleUri);

            //  Load the style XML in the part into an XDocument instance.
            XDocument styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));

            Console.WriteLine("TargetUri:{0}", styleRelation.TargetUri);
            Console.WriteLine("==================================================================");
            Console.WriteLine(styleDoc.Root);
            Console.WriteLine();
        }
    }
}
```

```vb
Const fileName As String = "SampleDoc.docx"

Const documentRelationshipType As String = _
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"
Const stylesRelationshipType As String = _
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"
Const wordmlNamespace As String = _
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main"
Dim w As XNamespace = wordmlNamespace

Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)
    Dim docPackageRelationship As PackageRelationship = _
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()
    If docPackageRelationship IsNot Nothing Then
        Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), _
          docPackageRelationship.TargetUri)
        Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)

        ' Load the document XML in the part into an XDocument instance.
        Dim xdoc As XDocument = XDocument.Load(XmlReader.Create(documentPart.GetStream()))

        Console.WriteLine("TargetUri:{0}", docPackageRelationship.TargetUri)
        Console.WriteLine("==================================================================")
        Console.WriteLine(xdoc.Root)
        Console.WriteLine()

        ' Find the styles part. There will only be one.
        Dim styleRelation As PackageRelationship = _
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()
        If styleRelation IsNot Nothing Then
            Dim styleUri As Uri = _
              PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)
            Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)

            ' Load the style XML in the part into an XDocument instance.
            Dim styleDoc As XDocument = XDocument.Load(XmlReader.Create(stylePart.GetStream()))

            Console.WriteLine("TargetUri:{0}", styleRelation.TargetUri)
            Console.WriteLine("==================================================================")
            Console.WriteLine(styleDoc.Root)
            Console.WriteLine()
        End If
    End If
End Using
```
