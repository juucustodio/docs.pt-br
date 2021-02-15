---
description: -recurse (opções do compilador C#)
title: -recurse (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /recurse
helpviewer_keywords:
- /recurse compiler option [C#]
- recurse compiler option [C#]
- -recurse compiler option [C#]
ms.assetid: 4e8212e5-04e3-45b1-8a42-41bc50e683b0
ms.openlocfilehash: 9e84ff95f7f0addac1c2c2d79af0ab53572da27f
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193797"
---
# <a name="-recurse-c-compiler-options"></a>-recurse (opções do compilador C#)

A opção -recurse permite compilar arquivos de código-fonte em todos os diretórios filho do diretório especificado (dir) ou do diretório do projeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-recurse:[dir\]file  
```  
  
## <a name="arguments"></a>Argumentos  

 `dir` (opcional)  
 O diretório no qual você deseja que a pesquisa comece. Se ele não for especificado, a pesquisa começará no diretório do projeto.  
  
 `file`  
 Os arquivos a serem pesquisados. São permitidos caracteres curinga.  
  
## <a name="remarks"></a>Comentários  

 A opção **-recurse** permite compilar arquivos de código-fonte em todos os diretórios filho do diretório especificado (`dir`) ou do diretório do projeto.  
  
 É possível usar curingas em um nome de arquivo para compilar todos os arquivos correspondentes no diretório do projeto sem usar **-recurse**.  
  
 Essa opção do compilador não está disponível no Visual Studio e não pode ser alterada programaticamente.  
  
## <a name="example"></a>Exemplo  

 Compila todos os arquivos C# no diretório atual:  
  
```console  
csc *.cs  
```  
  
 Compila todos os arquivos C# no diretório dir1\dir2 e quaisquer diretórios abaixo dele e gera dir2.dll:  
  
```console  
csc -target:library -out:dir2.dll -recurse:dir1\dir2\*.cs  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
