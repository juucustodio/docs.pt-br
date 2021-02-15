---
title: Como exibir o conteúdo do assembly
description: Você pode usar o desmontador IL para exibir os atributos e as referências de um assembly para outros módulos e assemblies.
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest, viewing information
- Ildasm.exe
- MSIL Disassembler
- assemblies [.NET], viewing contents
- viewing assembly information
- MSIL
- viewing MSIL information
ms.assetid: fb7baaab-4c0d-47ad-8fd3-4591cf834709
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: be2311c601effbebd519e33b7a5e13d49f44bd05
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687492"
---
# <a name="how-to-view-assembly-contents"></a>Como exibir o conteúdo do assembly

Você pode usar o [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) para exibir informações MSIL (Microsoft Intermediate Language) em um arquivo. Se o arquivo que está sendo examinado for um assembly, essas informações poderão incluir os atributos e as referências do assembly a outros módulos e assemblies. Essas informações podem ser úteis para determinar se um arquivo é um assembly ou parte de um assembly e se o arquivo tem referências a outros módulos ou assemblies.

Para exibir o conteúdo de um assembly usando *Ildasm.exe* , insira **ILDASM \<assembly name>** em um prompt de comando. Por exemplo, o comando a seguir desmonta o assembly *Hello.exe* .

```cmd
ildasm Hello.exe
```

Para exibir informações de manifesto do assembly, clique duas vezes no ícone de **manifesto** na janela do desmontador MSIL.

## <a name="example"></a>Exemplo

O exemplo a seguir começa com um programa "Olá, Mundo" básico. Depois de compilar o programa, use *Ildasm.exe* para desmontar o assembly *Hello.exe* e exibir o manifesto do assembly.

```cpp
using namespace System;

class MainApp
{
public:
    static void Main()
    {
        Console::WriteLine("Hello World using C++/CLI!");
    }
};

int main()
{
    MainApp::Main();
}
```

```csharp
using System;

class MainApp
{
    public static void Main()
    {
        Console.WriteLine("Hello World using C#!");
    }
}
```

```vb
Class MainApp
    Public Shared Sub Main()
        Console.WriteLine("Hello World using Visual Basic!")
    End Sub
End Class
```

Executar o comando *ildasm.exe* no assembly de *Hello.exe* e clicar duas vezes no ícone de **manifesto** na janela do desmontador MSIL produz a seguinte saída:

```output
// Metadata version: v4.0.30319
.assembly extern mscorlib
{
  .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4..
  .ver 4:0:0:0
}
.assembly Hello
{
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 )
  .custom instance void [mscorlib]System.Runtime.CompilerServices.RuntimeCompatibilityAttribute::.ctor() = ( 01 00 01 00 54 02 16 57 72 61 70 4E 6F 6E 45 78   // ....T..WrapNonEx
                                                                                                             63 65 70 74 69 6F 6E 54 68 72 6F 77 73 01 )       // ceptionThrows.
  .hash algorithm 0x00008004
  .ver 0:0:0:0
}
.module Hello.exe
// MVID: {7C2770DB-1594-438D-BAE5-98764C39CCCA}
.imagebase 0x00400000
.file alignment 0x00000200
.stackreserve 0x00100000
.subsystem 0x0003       // WINDOWS_CUI
.corflags 0x00000001    //  ILONLY
// Image base: 0x00600000
```

A tabela a seguir descreve cada diretiva no manifesto do assembly do assembly *Hello.exe* usado no exemplo:

|Diretiva|Descrição|
|---------------|-----------------|
|**. assembly externo \<assembly name>**|Especifica outro assembly que contém itens referenciados pelo módulo atual (neste exemplo, `mscorlib`).|
|**. PublicKeyToken \<token>**|Especifica o token da chave real do assembly referenciado.|
|**. ver \<version number>**|Especifica o número de versão do assembly referenciado.|
|**. assembly \<assembly name>**|Especifica o nome do assembly.|
|**. algoritmo de hash \<int32 value>**|Especifica o algoritmo de hash usado.|
|**. ver \<version number>**|Especifica o número de versão do assembly.|
|**. módulo \<file name>**|Especifica o nome dos módulos que compõem o assembly. Neste exemplo, o assembly consiste em apenas um arquivo.|
|**. subsistema \<value>**|Especifica o ambiente de aplicativo necessário para o programa. Neste exemplo, o valor 3 indica que este executável é executado em um console.|
|**.corflags**|Atualmente, um campo reservado nos metadados.|

Um manifesto do assembly pode conter várias diretivas diferentes, dependendo do conteúdo do assembly. Para obter uma lista extensa das diretivas no manifesto do assembly, consulte a documentação do ECMA, especialmente a "partição II: definição de metadados e semântica" e "partição III: conjunto de instruções CIL":

- [Padrões ECMA C# e Common Language Infrastructure](../components.md#applicable-standards)
- [ECMA-335-Common Language Infrastructure (CLI) padrão](http://www.ecma-international.org/publications/standards/Ecma-335.htm)

## <a name="see-also"></a>Veja também

- [Domínios de aplicativo e assemblies](../../framework/app-domains/application-domains.md#application-domains-and-assemblies)
- [Tópicos de instruções sobre domínios de aplicativo e assemblies](../../framework/app-domains/application-domains-and-assemblies-how-to-topics.md)
- [Ildasm.exe (desmontador de IL)](../../framework/tools/ildasm-exe-il-disassembler.md)
