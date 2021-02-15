---
description: 'Saiba mais sobre: como consultar arquivos com um atributo ou nome especificado (Visual Basic)'
title: 'Como: consultar arquivos com um atributo ou um nome especificado'
ms.date: 07/20/2015
ms.assetid: b26026a3-3f43-448f-a582-259997af6be0
ms.openlocfilehash: 3eb58bf683b97c5806145395cb489f0e85c2071b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100425718"
---
# <a name="how-to-query-for-files-with-a-specified-attribute-or-name-visual-basic"></a>Como consultar arquivos com um atributo ou nome especificado (Visual Basic)

Este exemplo mostra como localizar todos os arquivos que têm uma extensão de nome de arquivo especificada (por exemplo ".txt") em uma árvore de diretório especificada. Ele também mostra como retornar tanto os arquivos mais recentes como os mais antigo na árvore com base na hora de criação.  
  
## <a name="example"></a>Exemplo  
  
```vb  
Module FindFileByExtension  
    Sub Main()  
  
        ' Change the drive\path if necessary  
        Dim root As String = "C:\Program Files\Microsoft Visual Studio 9.0"  
  
        'Take a snapshot of the folder contents  
        Dim dir As New System.IO.DirectoryInfo(root)  
  
        Dim fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories)  
  
        ' This query will produce the full path for all .txt files  
        ' under the specified folder including subfolders.  
        ' It orders the list according to the file name.  
        Dim fileQuery = From file In fileList _  
                        Where file.Extension = ".txt" _  
                        Order By file.Name _  
                        Select file  
  
        For Each file In fileQuery  
            Console.WriteLine(file.FullName)  
        Next  
  
        ' Create and execute a new query by using  
        ' the previous query as a starting point.  
        ' fileQuery is not executed again until the  
        ' call to Last  
        Dim fileQuery2 = From file In fileQuery _  
                         Order By file.CreationTime _  
                         Select file.Name, file.CreationTime  
  
        ' Execute the query  
        Dim newestFile = fileQuery2.Last  
  
        Console.WriteLine("\r\nThe newest .txt file is {0}. Creation time: {1}", _  
                newestFile.Name, newestFile.CreationTime)  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
  
    End Sub  
End Module  
```  
  
## <a name="compile-the-code"></a>Compilar o código  

Crie um projeto de aplicativo de console Visual Basic, com uma `Imports` instrução para o namespace System. Linq.
  
## <a name="see-also"></a>Consulte também

- [LINQ to Objects (Visual Basic)](linq-to-objects.md)
- [LINQ e diretórios de arquivos (Visual Basic)](linq-and-file-directories.md)
