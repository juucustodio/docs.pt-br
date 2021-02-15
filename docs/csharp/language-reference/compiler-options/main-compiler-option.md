---
description: -main (opções do compilador C#)
title: -main (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /main
helpviewer_keywords:
- -main compiler option [C#]
- main compiler option [C#]
- /main compiler option [C#]
ms.assetid: 975cf4d5-36ac-4530-826c-4aad0c7f2049
ms.openlocfilehash: c27898de2a7cc2f3c01c51f8de1122e81b2233b4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91194109"
---
# <a name="-main-c-compiler-options"></a>-main (opções do compilador C#)

Esta opção especifica a classe que contém o ponto de entrada para o programa, se mais de uma classe contiver um método **Main**.

## <a name="syntax"></a>Sintaxe

```console
-main:class
```

## <a name="arguments"></a>Argumentos

 `class`  
 O tipo que contém o método **Main**.  
 O nome de classe informado deve ser totalmente qualificado. Ele deve incluir o namespace completo que contém a classe, seguido do nome de classe. Por exemplo, quando o método `Main` é localizado dentro da classe `Program` no namespace `MyApplication.Core`, a opção do compilador deve ser `-main:MyApplication.Core.Program`.

## <a name="remarks"></a>Comentários

Se sua compilação incluir mais de um tipo com um método [Main](../../programming-guide/main-and-command-args/index.md), você poderá especificar qual tipo contém o método **Main** que deseja usar como o ponto de entrada para o programa.

Essa opção é para uso durante a compilação de um arquivo *. exe* .

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio

1. Abra a página **Propriedades** do projeto.

2. Clique na página de propriedades do **Aplicativo**.

3. Modifique a propriedade **Objeto de inicialização**.

    Para definir programaticamente essa opção do compilador, confira <xref:VSLangProj80.ProjectProperties3.StartupObject%2A>.

### <a name="to-set-this-compiler-option-by-manually-editing-the-csproj-file"></a>Para definir essa opção de compilador editando manualmente o arquivo *. csproj*

Você pode definir essa opção editando o arquivo. csproj e adicionando um elemento `StartupObject` dentro da `PropertyGroup` seção. Por exemplo:

```xml
  <PropertyGroup>
    ...
    <StartupObject>MyApplication.Core.Program</StartupObject>
  </PropertyGroup>
```

## <a name="example"></a>Exemplo

Compile `t2.cs` e `t3.cs`, especificando que o método **Main** será encontrado em `Test2`:

```console
csc t2.cs t3.cs -main:Test2
```

## <a name="see-also"></a>Veja também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
