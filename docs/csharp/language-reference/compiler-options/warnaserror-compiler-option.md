---
description: -warnaserror (opções do compilador C#)
title: -warnaserror (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /warnaserror
helpviewer_keywords:
- /warnaserror compiler option [C#]
- -warnaserror compiler option [C#]
- warnaserror compiler option [C#]
ms.assetid: 04680ec3-08d6-4e2e-a274-38310e10e33c
ms.openlocfilehash: 9c3b307668968865b401aedc04c79f95d4f32513
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91171332"
---
# <a name="-warnaserror-c-compiler-options"></a>-warnaserror (opções do compilador C#)

A opção **-warnaserror+** trata todos os avisos como erros  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-warnaserror[+ | -][:warning-list]  
```  
  
## <a name="remarks"></a>Comentários  

 Quaisquer mensagens que seriam, normalmente, ser relatadas como avisos, são relatadas como erros e o processo de build é interrompido (os arquivos de saída não são compilados).  
  
 Por padrão, a opção **-warnaserror-** está em vigor, o que faz com que os avisos não impeçam a geração de um arquivo de saída. A **-warnaserror**, que é a mesma que **-warnaserror+**, faz com que os avisos sejam tratados como erros.  
  
 Opcionalmente, se você deseja que apenas avisos específicos sejam tratados como erros, você pode especificar uma lista separada por vírgulas de números de aviso para serem tratados como erros. O conjunto de todos os avisos de nulidade pode ser especificado com a abreviação **anulável** .
  
 Use [-warn](./warn-compiler-option.md) para especificar o nível de avisos que você deseja que o compilador exiba. Use [-nowarn](./nowarn-compiler-option.md) para desabilitar determinados avisos.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto.  
  
2. Clique na página de propriedades **Compilar**.  
  
3. Modifique a propriedade **Tratar Avisos como Erros**.  
  
 Para definir programaticamente essa opção do compilador, confira <xref:VSLangProj80.CSharpProjectConfigurationProperties3.TreatWarningsAsErrors>.  
  
## <a name="example"></a>Exemplo  

 Compilar `in.cs` e fazer com que o compilador não exiba avisos:  
  
```console  
csc -warnaserror in.cs  
csc -warnaserror:642,649,652,nullable in.cs  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
