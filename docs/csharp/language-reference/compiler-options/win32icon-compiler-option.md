---
description: -win32icon (opções do compilador C#)
title: -win32icon (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /win32icon
helpviewer_keywords:
- win32icon compiler option [C#]
- /win32icon compiler option [C#]
- -win32icon compiler option [C#]
ms.assetid: 756d9b6d-ab07-41b7-ba58-5bd88f711138
ms.openlocfilehash: 5b62bbfe28bb5aa82605a88a83cf82eff9278807
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91168862"
---
# <a name="-win32icon-c-compiler-options"></a>-win32icon (opções do compilador C#)

A opção **-win32icon** insere um arquivo .ico no arquivo de saída, que fornece ao arquivo de saída a aparência desejada no Explorador de Arquivos.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-win32icon:filename  
```  
  
## <a name="arguments"></a>Argumentos  

 `filename`  
 O arquivo .ico que você deseja adicionar ao seu arquivo de saída.  
  
## <a name="remarks"></a>Comentários  

 Um arquivo .ico pode ser criado com o [Compilador de Recurso](/windows/desktop/menurc/resource-compiler). O Compilador de Recurso é invocado quando você compila um programa do Visual C++; um arquivo .ico é criado com base no arquivo .rc.  
  
 Consulte [-linkresource](./linkresource-compiler-option.md) (para referenciar) ou [-resource](./resource-compiler-option.md) (para anexar) um arquivo de recurso do .NET Framework. Consulte [-win32res](./win32res-compiler-option.md) para importar um arquivo. res.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página de **Propriedades** do projeto.  
  
2. Clique na página de propriedades do **Aplicativo**.  
  
3. Modifique a propriedade **Ícone do aplicativo**.  
  
 Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.ProjectProperties3.ApplicationIcon%2A>.  
  
## <a name="example"></a>Exemplo  

 Compilar `in.cs` e anexar um arquivo .ico `rf.ico` para produzir `in.exe`:  
  
```console  
csc -win32icon:rf.ico in.cs  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
