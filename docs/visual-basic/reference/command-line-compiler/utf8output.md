---
description: Saiba mais sobre:-utf8output (Visual Basic)
title: -utf8output
ms.date: 07/20/2015
helpviewer_keywords:
- -utf8output compiler option [Visual Basic]
- utf8output compiler option [Visual Basic]
- /utf8output compiler option [Visual Basic]
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
ms.openlocfilehash: 317c1be3f18150ae88bb8e95927d9f5faf0e4f3c
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100461886"
---
# <a name="-utf8output-visual-basic"></a>-utf8output (Visual Basic)

Exibe a saída do compilador usando a codificação UTF-8.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-utf8output[+ | -]  
```  
  
## <a name="arguments"></a>Argumentos  

 `+` &#124; `-`  
 Opcional. O padrão para essa opção é `-utf8output-` , que significa que a saída do compilador não usa a codificação UTF-8. Especificar `-utf8output` é o mesmo que especificar `-utf8output+` .  
  
## <a name="remarks"></a>Comentários  

 Em algumas configurações internacionais, a saída do compilador não pode ser exibida corretamente no console do. Nessas situações, use `-utf8output` e redirecione a saída do compilador para um arquivo.  
  
> [!NOTE]
> A `-utf8output` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ela está disponível somente durante a compilação na linha de comando.  
  
## <a name="example"></a>Exemplo  

 O código a seguir compila `In.vb` e direciona o compilador para exibir a saída usando a codificação UTF-8.  
  
```console  
vbc -utf8output in.vb  
```  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
