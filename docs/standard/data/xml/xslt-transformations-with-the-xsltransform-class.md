---
description: 'Saiba mais sobre: transformações XSLT com a classe XslTransform'
title: Transformações XSLT com a classe XslTransform
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 500335af-f9b5-413b-968a-e6d9a824478c
ms.openlocfilehash: f350bf8c27804afe769629bc1efdeb1bb51a2876
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99731910"
---
# <a name="xslt-transformations-with-the-xsltransform-class"></a>Transformações XSLT com a classe XslTransform

> [!NOTE]
> A classe <xref:System.Xml.Xsl.XslTransform> está obsoleta no .NET Framework 2.0. Você pode executar a linguagem XSL Transformations (XSLT) usando a classe <xref:System.Xml.Xsl.XslCompiledTransform>. Confira [Usar a classe XslCompiledTransform](using-the-xslcompiledtransform-class.md) e [Migrar da classe XslTransform](migrating-from-the-xsltransform-class.md) para saber mais.

O objetivo do XSLT é transformar o conteúdo de um documento XML de origem em outro documento que seja diferente no formato ou estrutura (por exemplo, para transformar XML em HTML para uso em um site ou para transformá-lo em um documento que contém somente os campos exigidos por um aplicativo). Este processo de transformação é especificado pela [recomendação de XSLT versão 1.0](https://www.w3.org/TR/1999/REC-xslt-19991116) do W3C (World Wide Web Consortium). No .NET Framework, a classe <xref:System.Xml.Xsl.XslTransform>, localizada no namespace <xref:System.Xml.Xsl> é o processador XSLT que implementa a funcionalidade dessa especificação. Há um pequeno número de recursos que não foram implementados da recomendação XSLT 1.0 do W3C, listada em [Saída de um XslTransform](outputs-from-an-xsltransform.md). A figura a seguir mostra a arquitetura de transformação do .NET Framework.

## <a name="overview"></a>Visão geral

![Diagrama que mostra a arquitetura de transformação XSLT.](./media/xslt-transformations-with-the-xsltransform-class/xslt-transformation-architecture.gif)

A recomendação XSLT usa a linguagem XPath para selecionar partes de um documento XML, onde XPath é uma linguagem de consulta usada para navegar em nós de uma árvore do documento. Conforme mostrado no diagrama, a implementação de XPath do .NET Framework é usada para selecionar partes de XML armazenadas em várias classes, como um <xref:System.Xml.XmlDocument>, um <xref:System.Xml.XmlDataDocument> e um <xref:System.Xml.XPath.XPathDocument>. Um <xref:System.Xml.XPath.XPathDocument> é um repositório de dados XSLT otimizado e, quando usado com <xref:System.Xml.Xsl.XslTransform>, fornece transformações XSLT com bom desempenho.

A seguinte tabela lista classes geralmente usadas ao trabalhar com o <xref:System.Xml.Xsl.XslTransform> e XPath e sua função.

|Classe ou interface|Função|
|------------------------|--------------|
|<xref:System.Xml.XPath.XPathNavigator>|É uma API que fornece um modelo de estilo de cursor para navegar em um repositório, junto com suporte a consulta XPath. Não fornece a edição do repositório subjacente. Para editar, use a classe <xref:System.Xml.XmlDocument>.|
|<xref:System.Xml.XPath.IXPathNavigable>|É uma interface que fornece um método `CreateNavigator` para um <xref:System.Xml.XPath.XPathNavigator> para o repositório.|
|<xref:System.Xml.XmlDocument>|Ela permite a edição deste documento. Implementa <xref:System.Xml.XPath.IXPathNavigable>, permitindo os cenários de edição de documento onde as transformações XSLT são necessárias posteriormente. Para saber mais, consulte [Entrada de XmlDocument para XslTransform](xmldocument-input-to-xsltransform.md).|
|<xref:System.Xml.XmlDataDocument>|É derivada do <xref:System.Xml.XmlDocument>. Ela faz a ponte sobre os mundos relacionais e XML usando <xref:System.Data.DataSet> para otimizar o armazenamento de dados estruturados dentro do documento XML de acordo com mapeamentos especificados no <xref:System.Data.DataSet>. Ela implementa <xref:System.Xml.XPath.IXPathNavigable>, permitindo situações onde as transformações XSLT podem ser executadas sobre os dados relacionais recuperados de um banco de dados. Para saber mais, confira [Integração XML com dados relacionais e ADO.NET](xml-integration-with-relational-data-and-adonet.md).|
|<xref:System.Xml.XPath.XPathDocument>|Essa classe é otimizada para processamento de <xref:System.Xml.Xsl.XslTransform> e consultas XPath, e fornece um cache somente leitura de alto desempenho. Implementa <xref:System.Xml.XPath.IXPathNavigable> e é o repositório preferido a ser usado para transformações XSLT.|
|<xref:System.Xml.XPath.XPathNodeIterator>|Fornece a navegação em conjuntos de nós XPath. Todos os métodos de seleção XPath no <xref:System.Xml.XPath.XPathNavigator> retornam um <xref:System.Xml.XPath.XPathNodeIterator>. Vários objetos <xref:System.Xml.XPath.XPathNodeIterator> podem ser criados no mesmo repositório, cada um representando um conjunto de nós selecionado.|

## <a name="msxml-xslt-extensions"></a>Extensões de MSXML XSLT

As funções `msxsl:script` e `msxsl:node-set` são as únicas extensões XSLT do Microsoft XML Core Services (MSXML) com suporte pela classe <xref:System.Xml.Xsl.XslTransform>.

## <a name="example"></a>Exemplo

O exemplo de código a seguir carrega uma folha de estilos XSLT, lê um arquivo chamado mydata.xml em um <xref:System.Xml.XPath.XPathDocument> e executa uma transformação nos dados em um arquivo fictício chamado myStyleSheet.xsl, enviando a saída formatada para o console.

```vb
Imports System.IO
Imports System.Xml
Imports System.Xml.XPath
Imports System.Xml.Xsl

Public Class Sample
    Private filename As [String] = "mydata.xml"
    Private stylesheet As [String] = "myStyleSheet.xsl"

    Public Shared Sub Main()
        Dim xslt As New XslTransform()
        xslt.Load(stylesheet)
        Dim xpathdocument As New XPathDocument(filename)
        Dim writer As New XmlTextWriter(Console.Out)
        writer.Formatting = Formatting.Indented

        xslt.Transform(xpathdocument, Nothing, writer, Nothing)
    End Sub 'Main
End Class 'Sample
```

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.XPath;
using System.Xml.Xsl;

public class Sample
{
    private const String filename = "mydata.xml";
    private const String stylesheet = "myStyleSheet.xsl";

    public static void Main()
    {
        XslTransform xslt = new XslTransform();
        xslt.Load(stylesheet);
        XPathDocument xpathdocument = new XPathDocument(filename);
        XmlTextWriter writer = new XmlTextWriter(Console.Out);
        writer.Formatting = Formatting.Indented;

        xslt.Transform(xpathdocument, null, writer, null);
    }
}
```

## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Xsl.XslTransform>
- [A classe XslTransform implementa do processador XSLT](xsltransform-class-implements-the-xslt-processor.md)
- [Implementação de comportamentos arbitrários na classe XslTransform](implementation-of-discretionary-behaviors-in-the-xsltransform-class.md)
- [XPathNavigator nas transformações](xpathnavigator-in-transformations.md)
- [XPathNodeIterator nas transformações](xpathnodeiterator-in-transformations.md)
- [XPathDocument inseriu a XslTransform](xpathdocument-input-to-xsltransform.md)
- [XmlDataDocument inseriu a XslTransform](xmldatadocument-input-to-xsltransform.md)
- [XmlDocument inseriu a XslTransform](xmldocument-input-to-xsltransform.md)
