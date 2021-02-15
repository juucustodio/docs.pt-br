---
description: -target:winmdobj (opções do compilador C#)
title: -target:winmdobj (opções do compilador C#)
ms.date: 07/20/2015
ms.assetid: 1819a045-659d-498a-9457-c466e902986f
ms.openlocfilehash: a13e2da02698209a514e716d65c1df3508cf1508
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91171397"
---
# <a name="-targetwinmdobj-c-compiler-options"></a>-target:winmdobj (opções do compilador C#)

Se você usar a opção do compilador **-target:winmdobj**, o compilador criará um arquivo .winmdobj intermediário que pode ser convertido em um arquivo binário do Windows Runtime (.winmd). O arquivo .winmd pode, então, ser consumido por programas JavaScript e C++, bem como programas de linguagem gerenciada.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-target:winmdobj  
```  
  
## <a name="remarks"></a>Comentários  

 A configuração **winmdobj** indica para o compilador que um módulo intermediário é necessário. Em resposta, o Visual Studio compila a biblioteca de classes do C# como um arquivo .winmdobj. O arquivo .winmdobj pode, então, ser alimentado por meio da ferramenta de exportação <xref:Microsoft.Build.Tasks.WinMDExp> para produzir um arquivo de metadados do Windows (.winmd). O arquivo .winmd contém o código da biblioteca original e os metadados do WinMD que são usados pelo JavaScript ou C++ e pelo Windows Runtime.  
  
 A saída de um arquivo que é compilado usando a opção do compilador **-target:winmdobj** foi criada para ser usada apenas como entrada para a ferramenta de exportação WimMDExp. O arquivo .winmdobj em si não é referenciado diretamente.  
  
 A menos que você use a opção [-out](./out-compiler-option.md), o nome do arquivo de saída usará o nome do primeiro arquivo de entrada. Um método [Main](../../programming-guide/main-and-command-args/index.md) não é necessário.  
  
 Se você especificar a opção -target:winmdobj em um prompt de comando, todos os arquivos até a próxima opção **-out** ou [-target:module](./target-module-compiler-option.md) serão usados para criar o programa do Windows.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-ide-for-a-windows-store-app"></a>Para definir esta opção de compilador no IDE do Visual Studio para um aplicativo da Windows Store  
  
1. No **Gerenciador de Soluções**, abra o menu de atalho do projeto e escolha **Propriedades**.  
  
2. Escolha a guia **Aplicativo**.  
  
3. Na lista **Tipo de saída**, escolha **Arquivo WinMD**.  
  
     A opção de **arquivo WinMD** está disponível somente para modelos de aplicativo da loja do Windows 8. x.  
  
 Para saber mais sobre como definir essa opção do compilador programaticamente, veja <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Exemplo  

 O comando a seguir compila `filename.cs` em um arquivo .winmdobj intermediário.  
  
```console  
csc -target:winmdobj filename.cs  
```  
  
## <a name="see-also"></a>Confira também

- [-Target (opções do compilador C#)](./target-compiler-option.md)
- [Opções do compilador de C#](./index.md)
