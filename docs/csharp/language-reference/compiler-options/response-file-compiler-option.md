---
description: '@ (Opções do compilador de C#)'
title: '@ (Opções do compilador de C#)'
ms.date: 07/20/2015
f1_keywords:
- '@'
helpviewer_keywords:
- response files, specifying for compilation [C#]
- '@ compiler option'
ms.assetid: dda4fa9f-a02c-400f-8b6a-d58834e13d7f
ms.openlocfilehash: 8f7e222e194fc4ba96159ecd792765f64b4d1c57
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91193745"
---
# <a name="-c-compiler-options"></a>@ (Opções do compilador de C#)

A opção @ possibilita especificar um arquivo que contém opções do compilador e arquivos de código-fonte a serem compilados.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
@response_file  
```  
  
## <a name="arguments"></a>Argumentos  

 `response_file`  
 Um arquivo que lista as opções do compilador ou os arquivos de código-fonte a serem compilados.  
  
## <a name="remarks"></a>Comentários  

 As opções do compilador e os arquivos de código-fonte serão processados pelo compilador apenas se eles tiverem sido especificados na linha de comando.  
  
 Para especificar mais de um arquivo de resposta em uma compilação, especifique várias opções de arquivo de resposta. Por exemplo:  
  
```console  
@file1.rsp @file2.rsp  
```  
  
 Em um arquivo de resposta, várias opções de compilador e de arquivos de código-fonte podem ser exibidas em uma linha. Uma única especificação de opção do compilador deve ser exibida em uma linha (não é possível abranger várias linhas). Os arquivos de resposta podem ter comentários que começam com o símbolo #.  
  
 Especificar opções do compilador de dentro de um arquivo de resposta é como emitir esses comandos na linha de comando. Consulte [Compilando da linha de comando](./how-to-set-environment-variables-for-the-visual-studio-command-line.md) para obter mais informações.  
  
 O compilador processa as opções de comando como elas são encontradas. Portanto, os argumentos da linha de comando podem substituir opções listadas anteriormente em arquivos de resposta. Por outro lado, opções em um arquivo de resposta substituirão as opções listadas anteriormente na linha de comando ou em outros arquivos de resposta.  
  
 O C# fornece o arquivo csc.rsp, localizado no mesmo diretório que o arquivo csc.exe. Consulte [-noconfig](./noconfig-compiler-option.md) para obter mais informações sobre CSC. rsp.  
  
 Essa opção do compilador não pode ser definida no ambiente de desenvolvimento do Visual Studio nem pode ser alterada por meio de programação.  
  
## <a name="example"></a>Exemplo  

 A seguir, há algumas linhas de um exemplo de arquivo de resposta:  
  
```console  
# build the first output file  
-target:exe -out:MyExe.exe source1.cs source2.cs  
```  
  
## <a name="see-also"></a>Veja também

- [Opções do compilador de C#](./index.md)
