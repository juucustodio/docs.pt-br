---
title: Como dividir um arquivo em vários arquivos usando grupos (LINQ) (C#)
description: Saiba como dividir um arquivo em vários arquivos usando grupos. Consulte um exemplo de código e exiba recursos adicionais disponíveis.
ms.date: 07/20/2015
ms.assetid: 8179b91c-d778-4e57-884f-77fe5a8e4e40
ms.openlocfilehash: b7be01be0f1539eb6ed4f4857af2625672319493
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203924"
---
# <a name="how-to-split-a-file-into-many-files-by-using-groups-linq-c"></a>Como dividir um arquivo em vários arquivos usando grupos (LINQ) (C#)

Este exemplo mostra uma maneira de mesclar o conteúdo de dois arquivos e, em seguida, criar um conjunto de novos arquivos que organizam os dados em uma nova forma.  
  
### <a name="to-create-the-data-files"></a>Para criar os arquivos de dados  
  
1. Copie esses nomes em um arquivo de texto chamado names1.txt e salve-o na sua pasta do projeto:  
  
    ```text  
    Bankov, Peter  
    Holm, Michael  
    Garcia, Hugo  
    Potra, Cristina  
    Noriega, Fabricio  
    Aw, Kam Foo  
    Beebe, Ann  
    Toyoshima, Tim  
    Guy, Wey Yuan  
    Garcia, Debra  
    ```  
  
2. Copie esses nomes em um arquivo de texto chamado names2.txt e salve-o na sua pasta do projeto: observe que os dois arquivos têm alguns nomes em comum.  
  
    ```text  
    Liu, Jinghao  
    Bankov, Peter  
    Holm, Michael  
    Garcia, Hugo  
    Beebe, Ann  
    Gilchrist, Beth  
    Myrcha, Jacek  
    Giakoumakis, Leo  
    McLin, Nkenge  
    El Yassir, Mehdi  
    ```  
  
## <a name="example"></a>Exemplo  
  
```csharp  
class SplitWithGroups  
{  
    static void Main()  
    {  
        string[] fileA = System.IO.File.ReadAllLines(@"../../../names1.txt");  
        string[] fileB = System.IO.File.ReadAllLines(@"../../../names2.txt");  
  
        // Concatenate and remove duplicate names based on  
        // default string comparer  
        var mergeQuery = fileA.Union(fileB);  
  
        // Group the names by the first letter in the last name.  
        var groupQuery = from name in mergeQuery  
                         let n = name.Split(',')  
                         group name by n[0][0] into g  
                         orderby g.Key  
                         select g;  
  
        // Create a new file for each group that was created  
        // Note that nested foreach loops are required to access  
        // individual items with each group.  
        foreach (var g in groupQuery)  
        {  
            // Create the new file name.  
            string fileName = @"../../../testFile_" + g.Key + ".txt";  
  
            // Output to display.  
            Console.WriteLine(g.Key);  
  
            // Write file.  
            using (System.IO.StreamWriter sw = new System.IO.StreamWriter(fileName))  
            {  
                foreach (var item in g)  
                {  
                    sw.WriteLine(item);  
                    // Output to console for example purposes.  
                    Console.WriteLine("   {0}", item);  
                }  
            }  
        }  
        // Keep console window open in debug mode.  
        Console.WriteLine("Files have been written. Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:
    A  
       Aw, Kam Foo  
    B  
       Bankov, Peter  
       Beebe, Ann  
    E  
       El Yassir, Mehdi  
    G  
       Garcia, Hugo  
       Guy, Wey Yuan  
       Garcia, Debra  
       Gilchrist, Beth  
       Giakoumakis, Leo  
    H  
       Holm, Michael  
    L  
       Liu, Jinghao  
    M  
       Myrcha, Jacek  
       McLin, Nkenge  
    N  
       Noriega, Fabricio  
    P  
       Potra, Cristina  
    T  
       Toyoshima, Tim  
 */  
```  
  
 O programa grava um arquivo separado para cada grupo na mesma pasta que os arquivos de dados.  
  
## <a name="compiling-the-code"></a>Compilando o código

Criar um projeto de aplicativo de console em C# com diretivas `using` para os namespaces System.Linq e System.IO.
  
## <a name="see-also"></a>Veja também

- [LINQ e cadeias de caracteres (C#)](./linq-and-strings.md)
- [LINQ e diretórios de arquivos (C#)](./linq-and-file-directories.md)
