---
description: Saiba mais sobre:-nowin32manifest (Visual Basic)
title: -nowin32manifest
ms.date: 03/13/2018
helpviewer_keywords:
- /nowin32manifest compiler option [Visual Basic]
- nowin32manifest compiler option [Visual Basic]
- -nowin32manifest compiler option [Visual Basic]
ms.assetid: c0528aae-83b3-4425-99f0-19448e9843e3
ms.openlocfilehash: 3aa07ee26e47d48da69f1d1b34c8ec4643b7422e
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100426714"
---
# <a name="-nowin32manifest-visual-basic"></a>-nowin32manifest (Visual Basic)

Instrui o compilador a não inserir nenhum manifesto de aplicativo no arquivo executável.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-nowin32manifest  
```  
  
## <a name="remarks"></a>Comentários  

 Quando essa opção for usada, o aplicativo estará sujeito à virtualização no Windows Vista, a menos que você forneça um manifesto do aplicativo em um arquivo de recurso Win32 ou durante uma etapa de build posterior. Para saber mais sobre virtualização, confira [Implantação do ClickOnce no Windows Vista](/visualstudio/deployment/clickonce-deployment-on-windows-vista).  
  
 Para saber mais sobre a criação do manifesto, confira [-win32manifest (Visual Basic)](win32manifest.md).  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [Página de Aplicativo, Designer de Projeto (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
