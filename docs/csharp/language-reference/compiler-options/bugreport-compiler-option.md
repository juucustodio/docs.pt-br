---
description: -bugreport (opções do compilador C#)
title: -bugreport (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /bugreport
helpviewer_keywords:
- /bugreport compiler option [C#]
- -bugreport compiler option [C#]
- bugreport compiler option [C#]
ms.assetid: f39665e3-4f6f-4357-88a2-3274c7bec0c1
ms.openlocfilehash: 1fb2efc9b12680e95767746c7e4e1ddacbdd2594
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "93281500"
---
# <a name="-bugreport-c-compiler-options"></a>-bugreport (opções do compilador C#)

Especifica que as informações de depuração devem ser colocadas em um arquivo para análise posterior.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-bugreport:file  
```  
  
## <a name="arguments"></a>Argumentos  

 `file`  
 O nome do arquivo que conterá o relatório de bug.  
  
## <a name="remarks"></a>Comentários  

 A opção **-bugreport** especifica que as informações a seguir devem ser colocadas em `file`:  
  
- Uma cópia de todos os arquivos de código-fonte na compilação.  
  
- Uma lista das opção do compilador usadas na compilação.  
  
- Informações de versão sobre o compilador, o tempo de execução e o sistema operacional.  
  
- Assemblies e módulos referenciados, salvos como dígitos hexadecimais, exceto assemblies que são fornecidos com o .NET e o SDK do .NET.  
  
- Saída do compilador, se houver.  
  
- Uma solicitação de descrição do problema.  
  
- Uma solicitação de como você acha que o problema deve ser corrigido.  
  
 Se essa opção for usada com **-errorreport:prompt** ou **-errorreport:send**, as informações no arquivo serão enviadas à Microsoft Corporation.  
  
 Como uma cópia de todos os arquivos de código-fonte será colocada no `file`, talvez seja desejável reproduzir o suposto defeito do código no programa mais curto possível.  
  
 Essa opção do compilador não está disponível no Visual Studio e não pode ser alterada programaticamente.  
  
 Observe que os conteúdos do arquivo gerado expõem o código-fonte, o que pode resultar na divulgação acidental de informações.  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [-ERRORREPORT (opções do compilador C#)](./errorreport-compiler-option.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
