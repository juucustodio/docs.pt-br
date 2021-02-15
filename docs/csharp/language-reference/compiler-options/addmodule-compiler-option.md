---
description: -addmodule (opções do compilador C#)
title: -addmodule (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /addmodule
helpviewer_keywords:
- /addmodule compiler option [C#]
- -addmodule compiler option [C#]
- addmodule compiler option [C#]
ms.assetid: ed604546-0dc2-4bd4-9a3e-610a8d973e58
ms.openlocfilehash: ec72fc76b3d550029b1286f64b8f86e69e721468
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150564"
---
# <a name="-addmodule-c-compiler-options"></a>-addmodule (opções do compilador C#)

Essa opção adiciona um módulo criado com a opção target:module para a compilação atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-addmodule:file[;file2]  
```  
  
## <a name="arguments"></a>Argumentos  

 `file`, `file2`  
 Um arquivo de saída que contém metadados. O arquivo não pode conter um manifesto do assembly. Para importar mais de um arquivo, separe os nomes de arquivo com vírgula ou ponto e vírgula.  
  
## <a name="remarks"></a>Comentários  

 Todos os módulos adicionados com **-addmodule** devem estar no mesmo diretório que o arquivo de saída em tempo de execução. Ou seja, é possível especificar um módulo em qualquer diretório em tempo de compilação, mas o módulo deve estar no diretório do aplicativo em tempo de execução. Se o módulo não estiver no diretório do aplicativo em tempo de execução, um <xref:System.TypeLoadException> será obtido.  
  
 `file` não pode conter um assembly. Por exemplo, se o arquivo de saída foi criado com [-target:module](./target-module-compiler-option.md), seus metadados podem ser importados com **-addmodule**.  
  
 Se o arquivo de saída tiver sido criado com uma opção **-target** diferente de **-target:module**, seus metadados não poderão ser importados com o **-addmodule**, mas poderão ser importados com [-reference](./reference-compiler-option.md).  
  
 Essa opção do compilador não está disponível no Visual Studio; um projeto não pode referenciar um módulo. Além disso, essa opção do compilador não pode ser alterada programaticamente.  
  
## <a name="example"></a>Exemplo  

 Compile o arquivo de origem `input.cs` e adicione metadados de `metad1.netmodule` e `metad2.netmodule` para produzir `out.exe`:  
  
```console  
csc -addmodule:metad1.netmodule;metad2.netmodule -out:out.exe input.cs  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
- [Assemblies de multiarquivo](../../../framework/app-domains/multifile-assemblies.md)
- [Como compilar um assembly de multiarquivos](../../../framework/app-domains/build-multifile-assembly.md)
