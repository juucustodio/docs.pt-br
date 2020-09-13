---
title: Criar o documento Office Open XML de origem-LINQ to XML
description: Saiba como criar o documento do Office Open XML WordprocessingML usado pelos outros exemplos neste tutorial.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 653c8cdb-73be-4dc2-927f-924cfb4ed9ed
ms.openlocfilehash: b3401d7309879661dcfc7062418ee75430dccf35
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551829"
---
# <a name="create-the-source-office-open-xml-document-linq-to-xml"></a>Criar o documento Office Open XML de origem (LINQ to XML)

Este artigo mostra como criar o documento do Office Open XML WordprocessingML usado pelos outros exemplos neste tutorial. Se você segue essas declarações, a saída corresponderão a saída fornecida em cada exemplo.

No entanto, os exemplos neste tutorial funcionarão com qualquer documento válido de WordprocessingML.

Para criar o documento que este tutorial usa, você precisa ter o Microsoft Office 2007 ou posterior instalado ou precisa ter o Microsoft Office 2003 com o Microsoft Office Compatibility Pack para formatos de arquivo do Word, Excel e PowerPoint 2007.

## <a name="create-the-wordprocessingml-document"></a>Criar o documento do WordprocessingML

Use as seguintes etapas para criar o documento do WordprocessingML:

1. Crie um novo documento Microsoft Word.
1. Cole o texto a seguir no novo documento.
   1. Para o C#, use este texto:

         ```text
         Parsing WordprocessingML with LINQ to XML

         The following example prints to the console.

         using System;

            class Program {
               public static void Main(string[] args) {
               Console.WriteLine("Hello World");
            }
         }

         This example produces the following output:

         Hello World
         ```

   1. Para Visual Basic, use este texto:

      ```text
      Parsing WordprocessingML with LINQ to XML

      The following example prints to the console.

      Imports System

      Class Program
         Public Shared  Sub Main(ByVal args() As String)
            Console.WriteLine("Hello World")
         End Sub
      End Class

      This example produces the following output:

      Hello World
      ```

1. Formatar a primeira linha com o estilo que dirige “1 ".
1. Para C#, selecione as linhas que contêm o código C#. A primeira linha começa com a palavra-chave `using` . A última linha é a chave da última. Formatar as linhas com a fonte de correio. Formatar-los com um novo estilo, e nomeie o novo estilo “código”.
1. Para Visual Basic, selecione as linhas que contêm o código de Visual Basic. A primeira linha começa com a palavra-chave `Imports` . A última linha é "End Class". Formatar as linhas com a fonte de correio. Formatar-los com um novo estilo, e nomeie o novo estilo “código”.
1. Finalmente, selecione a linha inteira que contém a saída, e formatar-la com o estilo de `Code` .
1. Salve o documento, e denomine-o SampleDoc.docx.

> [!NOTE]
> Se você estiver usando o Microsoft Word 2003, selecione **documento do word 2007** na lista suspensa **salvar como tipo** .

## <a name="see-also"></a>Confira também

- [Tutorial: manipular conteúdo em um documento do WordprocessingML](xml-shape-wordprocessingml-documents.md)
