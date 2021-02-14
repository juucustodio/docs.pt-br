---
description: Saiba mais sobre:-nologons (Visual Basic)
title: -nologo
ms.date: 03/13/2018
helpviewer_keywords:
- -nologo compiler option [Visual Basic]
- banners [Visual Basic], suppressing startup
- nologo compiler option [Visual Basic]
- /nologo compiler option [Visual Basic]
ms.assetid: 25ef54b6-d676-4639-a2d2-a747a158bc07
ms.openlocfilehash: 370889fbd5d4e499ba27ff8bee4adc16a7a71876
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100434882"
---
# <a name="-nologo-visual-basic"></a>-nologo (Visual Basic)

Suprime a exibição da faixa de direitos autorais e as mensagens informativas durante a compilação.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-nologo  
```  
  
## <a name="remarks"></a>Comentários  

 Se você especificar `-nologo` , o compilador não exibirá uma faixa de direitos autorais. Por padrão, `-nologo` não está em vigor.  
  
> [!NOTE]
> A `-nologo` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ela está disponível somente durante a compilação na linha de comando.  
  
## <a name="example"></a>Exemplo  

 O código a seguir compila `T2.vb` e não exibe uma faixa de direitos autorais.  
  
```console
vbc -nologo t2.vb  
```  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
