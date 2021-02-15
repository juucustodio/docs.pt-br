---
description: Saiba mais sobre:-Verbose
title: -verbose
ms.date: 03/13/2018
helpviewer_keywords:
- verbose compiler option [Visual Basic]
- -verbose compiler option [Visual Basic]
- /verbose compiler option [Visual Basic]
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
ms.openlocfilehash: ea222d4f284bcaf163b142269fe250a081b0ee4f
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100470130"
---
# <a name="-verbose"></a>-verbose

Faz com que o compilador produza mensagens de erro e status detalhados.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-verbose[+ | -]  
```  
  
## <a name="arguments"></a>Argumentos  

 `+` &#124; `-`  
 Opcional. Especificar `-verbose` é o mesmo que especificar `-verbose+` , o que faz com que o compilador emita mensagens detalhadas. O padrão para essa opção é `-verbose-` .  
  
## <a name="remarks"></a>Comentários  

 A `-verbose` opção exibe informações sobre o número total de erros emitidos pelo compilador, relata quais assemblies estão sendo carregados por um módulo e exibe quais arquivos estão sendo compilados no momento.  
  
> [!NOTE]
> A `-verbose` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ela está disponível somente durante a compilação na linha de comando.  
  
## <a name="example"></a>Exemplo  

 O código a seguir compila `In.vb` e direciona o compilador para exibir informações detalhadas de status.  
  
```console  
vbc -verbose in.vb  
```  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
