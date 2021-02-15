---
description: 'Saiba mais sobre: como gravar dados de objeto em um arquivo XML (Visual Basic)'
title: Como gravar dados de objeto em um arquivo XML
ms.date: 07/20/2015
ms.assetid: f7966480-5ed2-43ac-9894-33427436de2a
ms.openlocfilehash: c6935fa97ed8813528630f5794e0a8e3e7e77b4d
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100486830"
---
# <a name="how-to-write-object-data-to-an-xml-file-visual-basic"></a>Como gravar dados de objeto em um arquivo XML (Visual Basic)

Este exemplo grava o objeto de uma classe para um arquivo XML usando a classe <xref:System.Xml.Serialization.XmlSerializer>.  
  
## <a name="example"></a>Exemplo  
  
```vb  
Public Module XMLWrite  
  
    Sub Main()  
        WriteXML()  
    End Sub  
  
    Public Class Book  
        Public Title As String  
    End Class  
  
    Public Sub WriteXML()  
        Dim overview As New Book  
        overview.Title = "Serialization Overview"  
        Dim writer As New System.Xml.Serialization.XmlSerializer(GetType(Book))  
        Dim file As New System.IO.StreamWriter(  
            "c:\temp\SerializationOverview.xml")  
        writer.Serialize(file, overview)  
        file.Close()  
    End Sub  
End Module  
```  
  
## <a name="compile-the-code"></a>Compilar o código  

 A classe deve ter um construtor público sem parâmetros.  
  
## <a name="robust-programming"></a>Programação robusta  

 As seguintes condições podem causar uma exceção:  
  
- A classe que está sendo serializada não tem um construtor público sem parâmetros.  
  
- O arquivo existe e é somente leitura (<xref:System.IO.IOException>).  
  
- O caminho é muito longo (<xref:System.IO.PathTooLongException>).  
  
- O disco está cheio (<xref:System.IO.IOException>).  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  

 Este exemplo cria um novo arquivo, se o arquivo ainda não existe. Se um aplicativo precisar criar um arquivo, ele precisará de acesso `Create` para a pasta. Se o arquivo já existe, o aplicativo precisa apenas de acesso `Write`, um privilégio menor. Sempre que possível, é mais seguro criar o arquivo durante a implantação e somente conceder acesso `Read` a um único arquivo, em vez de acesso `Create` a uma pasta.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IO.StreamWriter>
- [Como ler dados de objeto de um arquivo XML (Visual Basic)](how-to-read-object-data-from-an-xml-file.md)
- [Serialização (Visual Basic)](index.md)
