---
description: -checked (opções do compilador C#)
title: -checked (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /checked
helpviewer_keywords:
- checked compiler option [C#]
- -checked compiler option [C#]
- /checked compiler option [C#]
ms.assetid: fb7475d3-e6a6-4e6d-b86c-69e7a74c854b
ms.openlocfilehash: c92ad61b2f482631230e0e6aeb0af5716a4fcb61
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91196826"
---
# <a name="-checked-c-compiler-options"></a>-checked (opções do compilador C#)

A opção **-checked** especifica se uma instrução de aritmética de inteiros que resulta em um valor fora do intervalo do tipo de dados e que não está no escopo de uma palavra-chave [checked](../keywords/checked.md) ou [unchecked](../keywords/unchecked.md), causa uma exceção de tempo de execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-checked[+ | -]  
```  
  
## <a name="remarks"></a>Comentários  

 Uma instrução de aritmética de inteiros que está no escopo de uma palavra-chave `checked` ou `unchecked` não está sujeita ao efeito da opção **-checked**.  
  
 Se uma instrução de aritmética de inteiros que não está no escopo de uma palavra-chave `checked` ou `unchecked` resultar em um valor fora do intervalo do tipo de dados e **-checked+** (ou **-checked**) for usado na compilação, a instrução causará uma exceção no tempo de execução. Se **-checked-** for usado na compilação, a instrução não causará uma exceção em tempo de execução.  
  
 O valor padrão para essa opção é **-checked-**. A verificação de estouro é desabilitada.

 Às vezes, as ferramentas automatizadas que são usadas para compilar grandes aplicativos definem -checked como +. Um cenário para uso de -checked- é substituir o padrão global da ferramenta especificando -checked-.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto. Para obter mais informações, consulte [Página Build, Designer de Projeto (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp).  
  
2. Clique na página de propriedades **Compilar**.  
  
3. Clique no botão **Avançado** .  
  
4. Modifique a propriedade **verificar estouro aritmético** .  
  
 Para acessar programaticamente essa opção do compilador, confira <xref:VSLangProj80.CSharpProjectConfigurationProperties3.CheckForOverflowUnderflow%2A>.  
  
## <a name="example"></a>Exemplo  

 O comando a seguir compila `t2.cs`. O uso de `-checked` no comando especifica que qualquer instrução de aritmética de inteiros no arquivo que não está no escopo de uma palavra-chave `checked` ou `unchecked` e que resulta em um valor fora do intervalo do tipo de dados, causa uma exceção em tempo de execução.  
  
```console  
csc t2.cs -checked  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
