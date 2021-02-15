---
title: Como classificar ou filtrar dados de texto por qualquer palavra ou campo (LINQ) (C#)
description: Saiba como classificar ou filtrar dados de texto por qualquer palavra ou campo. Veja um exemplo para classificar linhas de texto estruturado por qualquer campo na linha.
ms.date: 07/20/2015
ms.assetid: 7c04d42f-4a78-42c8-9ec8-57ef18fe13a9
ms.openlocfilehash: 05858cc787d3916b204910df10d3291796cebc02
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203937"
---
# <a name="how-to-sort-or-filter-text-data-by-any-word-or-field-linq-c"></a>Como classificar ou filtrar dados de texto por qualquer palavra ou campo (LINQ) (C#)

O exemplo a seguir mostra como classificar linhas de texto estruturado, como valores separados por vírgulas, por qualquer campo na linha. O campo pode ser especificado dinamicamente em runtime. Suponha que os campos em scores.csv representam o número de ID do aluno, seguido por uma série de quatro resultados de teste.  
  
### <a name="to-create-a-file-that-contains-data"></a>Para criar um arquivo que contém dados  
  
1. Copie os dados de scores.csv do tópico [como unir conteúdo de arquivos diferentes (LINQ) (C#)](./how-to-join-content-from-dissimilar-files-linq.md) e salve-o em sua pasta de solução.  
  
## <a name="example"></a>Exemplo  
  
```csharp  
public class SortLines  
{  
    static void Main()  
    {  
        // Create an IEnumerable data source  
        string[] scores = System.IO.File.ReadAllLines(@"../../../scores.csv");  
  
        // Change this to any value from 0 to 4.  
        int sortField = 1;  
  
        Console.WriteLine("Sorted highest to lowest by field [{0}]:", sortField);  
  
        // Demonstrates how to return query from a method.  
        // The query is executed here.  
        foreach (string str in RunQuery(scores, sortField))  
        {  
            Console.WriteLine(str);  
        }  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    // Returns the query variable, not query results!  
    static IEnumerable<string> RunQuery(IEnumerable<string> source, int num)  
    {  
        // Split the string and sort on field[num]  
        var scoreQuery = from line in source  
                         let fields = line.Split(',')  
                         orderby fields[num] descending  
                         select line;  
  
        return scoreQuery;  
    }  
}  
/* Output (if sortField == 1):  
   Sorted highest to lowest by field [1]:  
    116, 99, 86, 90, 94  
    120, 99, 82, 81, 79  
    111, 97, 92, 81, 60  
    114, 97, 89, 85, 82  
    121, 96, 85, 91, 60  
    122, 94, 92, 91, 91  
    117, 93, 92, 80, 87  
    118, 92, 90, 83, 78  
    113, 88, 94, 65, 91  
    112, 75, 84, 91, 39  
    119, 68, 79, 88, 92  
    115, 35, 72, 91, 70  
 */  
```  
  
 Este exemplo também demonstra como retornar uma variável de consulta de um método.  
  
## <a name="compiling-the-code"></a>Compilando o código  

Criar um projeto de aplicativo de console em C# com diretivas `using` para os namespaces System.Linq e System.IO.
  
## <a name="see-also"></a>Veja também

- [LINQ e cadeias de caracteres (C#)](./linq-and-strings.md)
