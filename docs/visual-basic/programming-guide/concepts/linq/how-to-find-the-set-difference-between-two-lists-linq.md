---
title: 'Como: localizar a diferença de conjunto entre duas listas (LINQ)'
ms.date: 07/20/2015
ms.assetid: b5b25474-10a8-4df6-aab5-75621bb6b68e
ms.openlocfilehash: 1671cd32c0c0b8a3ff7fa6be87bd43dde9750776
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91100211"
---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-visual-basic"></a>Como localizar a diferença de conjunto entre duas listas (LINQ) (Visual Basic)

Este exemplo mostra como usar o LINQ para comparar duas listas de cadeias de caracteres e retornar as linhas que estão no names1.txt, mas não no names2.txt.  
  
### <a name="to-create-the-data-files"></a>Para criar os arquivos de dados  
  
1. Copie names1.txt e names2.txt para a pasta da solução, conforme mostrado em [como: combinar e comparar as coleções de cadeias de caracteres (LINQ) (Visual Basic)](how-to-combine-and-compare-string-collections-linq.md).  
  
## <a name="example"></a>Exemplo  
  
```vb  
Class CompareLists  
  
    Shared Sub Main()  
  
        ' Create the IEnumerable data sources.  
        Dim names1 As String() = System.IO.File.ReadAllLines("../../../names1.txt")  
        Dim names2 As String() = System.IO.File.ReadAllLines("../../../names2.txt")  
  
        ' Create the query. Note that method syntax must be used here.  
        Dim differenceQuery = names1.Except(names2)  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt")  
  
        ' Execute the query.  
        For Each name As String In differenceQuery  
            Console.WriteLine(name)  
        Next  
  
        ' Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
End Class  
' Output:  
' The following lines are in names1.txt but not names2.txt  
' Potra, Cristina  
' Noriega, Fabricio  
' Aw, Kam Foo  
' Toyoshima, Tim  
' Guy, Wey Yuan  
' Garcia, Debra  
```  
  
 Alguns tipos de operações de consulta no Visual Basic, como <xref:System.Linq.Enumerable.Except%2A> , <xref:System.Linq.Enumerable.Distinct%2A> , <xref:System.Linq.Enumerable.Union%2A> e <xref:System.Linq.Enumerable.Concat%2A> , só podem ser expressos na sintaxe baseada em método.  
  
## <a name="compile-the-code"></a>Compilar o código  

Crie um projeto de aplicativo de console Visual Basic, com uma `Imports` instrução para o namespace System. Linq.
  
## <a name="see-also"></a>Confira também

- [LINQ e cadeias de caracteres (Visual Basic)](linq-and-strings.md)
