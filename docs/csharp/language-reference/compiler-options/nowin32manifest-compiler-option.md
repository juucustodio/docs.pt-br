---
description: -nowin32manifest (opções do compilador C#)
title: -nowin32manifest (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /nowin32manifest
helpviewer_keywords:
- nowin32manifest compiler option [C#]
- -nowin32manifest compiler option [C#]
- /nowin32manifest compiler option [C#]
ms.assetid: 6f06365b-b87b-46a2-b187-b3bfeaf4862d
ms.openlocfilehash: 13bbee66901149d54632d9b164431f8898cdf52e
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193992"
---
# <a name="-nowin32manifest-c-compiler-options"></a>-nowin32manifest (opções do compilador C#)

Use a opção **-nowin32manifest** para instruir o compilador a não inserir nenhum manifesto do aplicativo no arquivo executável.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-nowin32manifest  
```  
  
## <a name="remarks"></a>Comentários  

 Quando essa opção for usada, o aplicativo estará sujeito à virtualização no Windows Vista, a menos que você forneça um manifesto do aplicativo em um arquivo de recurso Win32 ou durante uma etapa de build posterior.  
  
 No Visual Studio, defina essa opção na página **Propriedade do Aplicativo** selecionando a opção **Criar aplicativo sem um manifesto** na lista suspensa **Manifesto**. Para obter mais informações, consulte [página do aplicativo, designer de projeto (C#)](/visualstudio/ide/reference/application-page-project-designer-csharp).  
  
 Para obter mais informações sobre a criação do manifesto, consulte [-win32manifest (Opções do compilador do C#)](./win32manifest-compiler-option.md).  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
