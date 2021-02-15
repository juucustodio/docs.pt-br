---
description: Saiba mais sobre:-Optimize
title: -optimize
ms.date: 07/20/2015
helpviewer_keywords:
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization [Visual Basic], enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
ms.openlocfilehash: 812eaa544dd874fd3871e58f366a34ee8176273a
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100426693"
---
# <a name="-optimize"></a>-optimize

Habilita ou desabilita as otimizações do compilador.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-optimize[ + | - ]  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|---|---|  
|`+` &#124; `-`|Opcional. A `-optimize-` opção desabilita otimizações de compilador. A `-optimize+` opção habilita otimizações. Por padrão, as otimizações estão desabilitadas.|  
  
## <a name="remarks"></a>Comentários  

 Otimizações do compilador tornam o arquivo de saída menor, mais rápido e mais eficiente. No entanto, como as otimizações resultam na reorganização de código no arquivo de saída, o `-optimize+` pode dificultar a depuração.  
  
 Todos os módulos gerados com `-target:module` para um assembly devem usar as mesmas `-optimize` configurações que o assembly. Para obter mais informações, consulte [-Target (Visual Basic)](target.md).  
  
 Você pode combinar as `-optimize` `-debug` Opções e.  
  
|Para definir-otimizar no ambiente de desenvolvimento integrado do Visual Studio|  
|---|  
|1. ter um projeto selecionado em **Gerenciador de soluções**. No menu **Projeto** , clique em **Propriedades**.<br />     <br />2. Clique na guia **Compilar** .<br />3. Clique no botão **avançado** .<br />4. modifique a caixa de seleção **habilitar otimizações** .|  
  
## <a name="example"></a>Exemplo  

 O código a seguir compila `T2.vb` e habilita as otimizações do compilador.  
  
```console
vbc t2.vb -optimize  
```  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [-debug (Visual Basic)](debug.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
- [-Target (Visual Basic)](target.md)
