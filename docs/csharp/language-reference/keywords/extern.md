---
description: Modificador extern – Referência de C#
title: Modificador extern – Referência de C#
ms.date: 07/20/2015
f1_keywords:
- extern_CSharpKeyword
- extern
helpviewer_keywords:
- DllImport attribute
- extern keyword [C#]
ms.assetid: 9c3f02c4-51b8-4d80-9cb2-f2b6e1ae15c7
ms.openlocfilehash: 25eb5e6642d8b608bedcb4e9adadde4d84c2bae9
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89138963"
---
# <a name="extern-c-reference"></a>extern (Referência de C#)

O modificador `extern` é usado para declarar um método implementado externamente. Um uso comum do modificador `extern` é com o atributo `DllImport` quando você está usando serviços Interop para chamar código não gerenciado. Nesse caso, o método também deve ser declarado como `static` conforme mostrado no seguinte exemplo:

```csharp
[DllImport("avifil32.dll")]
private static extern void AVIFileInit();
```

A palavra-chave `extern` também pode definir um alias de assembly externo que possibilita referenciar diferentes versões do mesmo componente de dentro de um único assembly. Para obter mais informações, consulte [alias externo](extern-alias.md).

É um erro usar os modificadores [abstract](abstract.md) e `extern` juntos para modificar o mesmo membro. Usar o modificador `extern` significa que esse método é implementado fora do código C#, enquanto que usar o modificador `abstract` significa que a implementação do método não é fornecida na classe.

A palavra-chave extern possui utilizações mais limitadas em C# do que em C++. Para comparar a palavra-chave de C# com a palavra-chave de C++, consulte Usando extern para especificar vínculos na referência da linguagem C++.

## <a name="example-1"></a>Exemplo 1

Neste exemplo, o programa recebe uma cadeia de caracteres do usuário e a exibe dentro de uma caixa de mensagem. O programa usa o método `MessageBox` importado da biblioteca User32.dll.

[!code-csharp[csrefKeywordsModifiers#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#8)]

## <a name="example-2"></a>Exemplo 2

Este exemplo ilustra um programa C# que chama uma biblioteca em C (uma DLL nativa).

1. Crie o seguinte arquivo em C e atribua o nome `cmdll.c`:

    ```c
    // cmdll.c
    // Compile with: -LD
    int __declspec(dllexport) SampleMethod(int i)
    {
      return i*10;
    }
    ```

2. Abra uma janela do Prompt de Comando de Ferramentas Nativas do Visual Studio x64 (ou x32) do diretório de instalação do Visual Studio e compile o arquivo `cmdll.c` digitando **cl -LD cmdll.c** no prompt de comando.

3. No mesmo diretório, crie o seguinte arquivo em C# e atribua o nome `cm.cs`:

    ```csharp
    // cm.cs
    using System;
    using System.Runtime.InteropServices;
    public class MainClass
    {
        [DllImport("Cmdll.dll")]
          public static extern int SampleMethod(int x);

        static void Main()
        {
            Console.WriteLine("SampleMethod() returns {0}.", SampleMethod(5));
        }
    }
    ```

4. Abra uma janela do Prompt de Comando de Ferramentas Nativas do Visual Studio x64 (ou x32) do diretório de instalação do Visual Studio e compile o arquivo `cm.cs` ao digitar:

    > **csc cm.cs** (para o prompt de comando do x64) – ou – **csc -platform:x86 cm.cs** (para o prompt de comando do x32)

    Isso criará o arquivo executável `cm.exe`.

5. Execute `cm.exe`. O método `SampleMethod` passa o valor 5 ao arquivo de DLL que retorna o valor multiplicado por 10.  O programa produz a seguinte saída:

    ```output
    SampleMethod() returns 50.
    ```

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Confira também

- <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=nameWithType>
- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Palavras-chave do C#](index.md)
- [Modificadores](index.md)
