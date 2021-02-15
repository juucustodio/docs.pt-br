---
description: -nowarn (opções do compilador C#)
title: -nowarn (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /nowarn
helpviewer_keywords:
- nowarn compiler option [C#]
- /nowarn compiler option [C#]
- -nowarn compiler option [C#]
ms.assetid: 6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4
ms.openlocfilehash: 31a7ee5eacb2e7cd6b24c4a2276ce6e07fcc67e1
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91194018"
---
# <a name="-nowarn-c-compiler-options"></a>-nowarn (opções do compilador C#)

A opção **-nowarn** permite suprimir a exibição de um ou mais avisos pelo compilador. Separe vários números de aviso com uma vírgula.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-nowarn:number1[,number2,...]  
```  
  
## <a name="arguments"></a>Argumentos  

 `number1`, `number2`  
 Números de aviso que você deseja que o compilador suprima.  
  
## <a name="remarks"></a>Comentários  

 Você só precisa especificar a parte numérica do identificador de aviso. Por exemplo, se quiser suprimir CS0028, você pode especificar `-nowarn:28`.  
  
 O compilador ignorará silenciosamente números de aviso passados para `-nowarn` que eram válidos em versões anteriores, mas que foram removidos do compilador. Por exemplo, CS0679 era válido no compilador no Visual Studio .NET 2002, mas foi removido posteriormente.  
  
 Os avisos a seguir não podem ser suprimidos pela opção `-nowarn`:  
  
- Aviso do compilador (nível 1) CS2002  
  
- Aviso do compilador (nível 1) CS2023  
  
- Aviso do compilador (nível 1) CS2029  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto. Para obter detalhes, consulte [Página de Build, Designer de Projeto (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp).  
  
2. Clique na página de propriedades **Compilar**.  
  
3. Modifique a propriedade **Suprimir Avisos**.  
  
 Para saber mais sobre como definir essa opção do compilador programaticamente, veja <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
- [Erros do compilador C#](../compiler-messages/index.md)
