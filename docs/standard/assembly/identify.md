---
title: Como determinar se um arquivo é um assembly
description: Este artigo mostra como determinar se um arquivo é um assembly .NET, manualmente e programaticamente.
ms.date: 08/19/2019
ms.assetid: ea5186bb-5bff-4dcb-bde9-d6ba4e2edd00
dev_langs:
- csharp
- vb
ms.openlocfilehash: b78acaad31996f8fc2b965f51f541e99aeceb111
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731495"
---
# <a name="how-to-determine-if-a-file-is-an-assembly"></a>Como determinar se um arquivo é um assembly

Um arquivo será um assembly somente se ele for gerenciado e se contiver uma entrada de assembly em seus metadados. Para obter mais informações sobre assemblies e metadados, consulte [manifesto do assembly](manifest.md).  
  
## <a name="how-to-manually-determine-if-a-file-is-an-assembly"></a>Como determinar manualmente se um arquivo é um assembly  
  
1. Inicie o [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md).  
  
2. Carregue o arquivo que você deseja testar.  
  
3. Se o **ILDASM** relatar que o arquivo não é um arquivo PE (executável portátil), então ele não será um assembly. Para obter mais informações, consulte o tópico [How to: View assembly Contents](view-contents.md).  
  
## <a name="how-to-programmatically-determine-if-a-file-is-an-assembly"></a>Como determinar programaticamente se um arquivo é um assembly  
  
1. Chame o método <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType>, passando o caminho do arquivo completo e o nome do arquivo que você está testando.  
  
2. Se uma exceção <xref:System.BadImageFormatException> é gerada, o arquivo não é um assembly.  
  
## <a name="example"></a>Exemplo  

Este exemplo testa uma DLL para verificar se ela é um assembly.  

```csharp
class TestAssembly  
{  
    static void Main()  
    {  
  
        try  
        {  
            System.Reflection.AssemblyName testAssembly =  
                System.Reflection.AssemblyName.GetAssemblyName(@"C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll");  
  
            System.Console.WriteLine("Yes, the file is an assembly.");  
        }  
  
        catch (System.IO.FileNotFoundException)  
        {  
            System.Console.WriteLine("The file cannot be found.");  
        }  
  
        catch (System.BadImageFormatException)  
        {  
            System.Console.WriteLine("The file is not an assembly.");  
        }  
  
        catch (System.IO.FileLoadException)  
        {  
            System.Console.WriteLine("The assembly has already been loaded.");  
        }  
    }  
}  
/* Output (with .NET Framework 3.5 installed):  
    Yes, the file is an assembly.  
*/  
```  

```vb  
Module Module1  
    Sub Main()  
        Try  
            Dim testAssembly As Reflection.AssemblyName =  
                                Reflection.AssemblyName.GetAssemblyName("C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll")  
            Console.WriteLine("Yes, the file is an Assembly.")  
        Catch ex As System.IO.FileNotFoundException  
            Console.WriteLine("The file cannot be found.")  
        Catch ex As System.BadImageFormatException  
            Console.WriteLine("The file is not an Assembly.")  
        Catch ex As System.IO.FileLoadException  
            Console.WriteLine("The Assembly has already been loaded.")  
        End Try  
        Console.ReadLine()  
    End Sub  
End Module  
' Output (with .NET Framework 3.5 installed):  
'        Yes, the file is an Assembly.  
```

O método <xref:System.Reflection.AssemblyName.GetAssemblyName%2A> carrega o arquivo de teste e o libera quando a informação é lida.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Reflection.AssemblyName>
- [Guia de programação em C#](../../csharp/programming-guide/index.md)
- [Conceitos de programação (Visual Basic)](../../visual-basic/programming-guide/concepts/index.md)
- [Assemblies no .NET](index.md)
