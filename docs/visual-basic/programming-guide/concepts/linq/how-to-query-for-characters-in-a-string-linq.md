---
description: 'Saiba mais sobre: como consultar caracteres em uma cadeia (LINQ) (Visual Basic)'
title: 'Como: consultar caracteres em uma cadeia de caracteres (LINQ)'
ms.date: 07/20/2015
ms.assetid: 499ebbe0-746c-4235-9dba-ce722c12b50e
ms.openlocfilehash: bd8fabc06e88c83ae4e89079378ad67efb13c446
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100425744"
---
# <a name="how-to-query-for-characters-in-a-string-linq-visual-basic"></a>Como: consultar caracteres em uma cadeia de caracteres (LINQ) (Visual Basic)

Já que a classe <xref:System.String> implementa a interface <xref:System.Collections.Generic.IEnumerable%601> genérica, qualquer cadeia de caracteres pode ser consultada como uma sequência de caracteres. No entanto, esse não é um uso comum da LINQ. Para operações de correspondência de padrões complexas, use a classe <xref:System.Text.RegularExpressions.Regex>.

## <a name="example"></a>Exemplo

O exemplo a seguir consulta uma cadeia de caracteres para determinar quantos dígitos numéricos ela contém. Observe que a consulta é "reutilizada" depois que é executada pela primeira vez. Isso é possível porque a consulta em si não armazena nenhum resultado real.

```vb
Class QueryAString

    Shared Sub Main()

        ' A string is an IEnumerable data source.
        Dim aString As String = "ABCDE99F-J74-12-89A"

        ' Select only those characters that are numbers
        Dim stringQuery = From ch In aString
                          Where Char.IsDigit(ch)
                          Select ch
        ' Execute the query
        For Each c As Char In stringQuery
            Console.Write(c & " ")
        Next

        ' Call the Count method on the existing query.
        Dim count As Integer = stringQuery.Count()
        Console.WriteLine(System.Environment.NewLine & "Count = " & count)

        ' Select all characters before the first '-'
        Dim stringQuery2 = aString.TakeWhile(Function(c) c <> "-")

        ' Execute the second query
        For Each ch In stringQuery2
            Console.Write(ch)
        Next

        Console.WriteLine(System.Environment.NewLine & "Press any key to exit")
        Console.ReadKey()
    End Sub
End Class
' Output:
' 9 9 7 4 1 2 8 9
' Count = 8
' ABCDE99F
```

## <a name="compile-the-code"></a>Compilar o código

Crie um projeto de aplicativo de console Visual Basic, com uma `Imports` instrução para o namespace System. Linq.

## <a name="see-also"></a>Consulte também

- [LINQ e cadeias de caracteres (Visual Basic)](linq-and-strings.md)
- [Como combinar consultas LINQ com expressões regulares (Visual Basic)](how-to-combine-linq-queries-with-regular-expressions.md)
