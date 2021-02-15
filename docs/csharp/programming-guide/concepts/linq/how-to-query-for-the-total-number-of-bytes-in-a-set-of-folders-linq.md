---
title: Como consultar o número total de bytes em um conjunto de pastas (LINQ) (C#)
description: Saiba como usar o LINQ em C# para localizar o número total de bytes usados por todos os arquivos em uma pasta especificada e suas subpastas.
ms.date: 07/20/2015
ms.assetid: a01bd1d4-133c-4ca2-aa4e-e93e81d6076c
ms.openlocfilehash: 562fd32ad9e9040a5898322d840718f25b56e2cd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91159027"
---
# <a name="how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders-linq-c"></a>Como consultar o número total de bytes em um conjunto de pastas (LINQ) (C#)

Este exemplo mostra como recuperar o número total de bytes usado por todos os arquivos em uma pasta especificada e todas as suas subpastas.  
  
## <a name="example"></a>Exemplo  

 O método <xref:System.Linq.Enumerable.Sum%2A> adiciona os valores de todos os itens selecionados na cláusula `select`. Você pode modificar essa consulta para recuperar o maior ou o menor arquivo na árvore de diretório especificada chamando o método <xref:System.Linq.Enumerable.Min%2A> ou <xref:System.Linq.Enumerable.Max%2A> em vez de <xref:System.Linq.Enumerable.Sum%2A>.  
  
```csharp  
class QuerySize  
{  
    public static void Main()  
    {  
        string startFolder = @"c:\program files\Microsoft Visual Studio 9.0\VC#";  
  
        // Take a snapshot of the file system.  
        // This method assumes that the application has discovery permissions  
        // for all folders under the specified path.  
        IEnumerable<string> fileList = System.IO.Directory.GetFiles(startFolder, "*.*", System.IO.SearchOption.AllDirectories);  
  
        var fileQuery = from file in fileList  
                        select GetFileLength(file);  
  
        // Cache the results to avoid multiple trips to the file system.  
        long[] fileLengths = fileQuery.ToArray();  
  
        // Return the size of the largest file  
        long largestFile = fileLengths.Max();  
  
        // Return the total number of bytes in all the files under the specified folder.  
        long totalBytes = fileLengths.Sum();  
  
        Console.WriteLine("There are {0} bytes in {1} files under {2}",  
            totalBytes, fileList.Count(), startFolder);  
        Console.WriteLine("The largest files is {0} bytes.", largestFile);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit.");  
        Console.ReadKey();  
    }  
  
    // This method is used to swallow the possible exception  
    // that can be raised when accessing the System.IO.FileInfo.Length property.  
    static long GetFileLength(string filename)  
    {  
        long retval;  
        try  
        {  
            System.IO.FileInfo fi = new System.IO.FileInfo(filename);  
            retval = fi.Length;  
        }  
        catch (System.IO.FileNotFoundException)  
        {  
            // If a file is no longer present,  
            // just add zero bytes to the total.  
            retval = 0;  
        }  
        return retval;  
    }  
}  
```  
  
 Se precisar apenas contar o número de bytes em uma árvore de diretório especificada, você pode fazer isso com mais eficiência sem criar uma consulta LINQ, que gera a sobrecarga de criação da coleção de lista como uma fonte de dados. A utilidade da abordagem da LINQ aumenta conforme a consulta se torna mais complexa ou quando você precisa executar várias consultas na mesma fonte de dados.  
  
 A consulta chama um método separado para obter o tamanho de arquivo. Ela faz isso para consumir a possível exceção que será gerada se o arquivo tiver sido excluído em outro thread após o objeto <xref:System.IO.FileInfo> ter sido criado na chamada para `GetFiles`. Embora o objeto <xref:System.IO.FileInfo> já tenha sido criado, a exceção poderá ocorrer porque um objeto <xref:System.IO.FileInfo> tentará atualizar sua propriedade <xref:System.IO.FileInfo.Length%2A> com o tamanho mais atual na primeira vez que a propriedade foi acessada. Ao colocar essa operação em um bloco try-catch fora da consulta, o código segue a regra de evitar operações em consultas que podem causar efeitos colaterais. Em geral, deve-se ter muito cuidado ao consumir exceções para garantir que um aplicativo não seja deixado em um estado desconhecido.  
  
## <a name="compiling-the-code"></a>Compilando o código  

Criar um projeto de aplicativo de console em C# com diretivas `using` para os namespaces System.Linq e System.IO.
  
## <a name="see-also"></a>Confira também

- [LINQ to Objects (C#)](./linq-to-objects.md)
- [LINQ e diretórios de arquivos (C#)](./linq-and-file-directories.md)
