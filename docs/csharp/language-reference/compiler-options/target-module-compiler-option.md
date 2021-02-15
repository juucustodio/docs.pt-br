---
description: -target:module (opções do compilador C#)
title: -target:module (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /target:module
helpviewer_keywords:
- -target compiler options [C#], /target:module
- target compiler options [C#], /target:module
- /target compiler options [C#], /target:module
ms.assetid: 9af1e4fa-c749-44e7-ae58-90a3d05d4e72
ms.openlocfilehash: d8691e5e4477dbbe989344469b44382d5e0e7c8b
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193602"
---
# <a name="-targetmodule-c-compiler-options"></a>-target:module (opções do compilador C#)

Essa opção faz com que o compilador não gere um manifesto do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-target:module  
```  
  
## <a name="remarks"></a>Comentários  

 Por padrão, o arquivo de saída criado por meio da compilação com essa opção terá uma extensão .netmodule.  
  
 Um arquivo que não tem um manifesto do assembly não pode ser carregado pelo tempo de execução do .NET. No entanto, esse arquivo pode ser incorporado no manifesto do assembly de um assembly por meio de [-addmodule](./addmodule-compiler-option.md).  
  
 Se mais de um módulo for criado em uma única compilação, tipos [internos](../keywords/internal.md) em um módulo estarão disponíveis para outros módulos na compilação. Quando o código em um módulo referenciar tipos `internal` em outro módulo, os dois módulos deverão ser incorporados em um manifesto do assembly, por meio de **-addmodule**.  
  
 Não há suporte para a criação de um módulo no ambiente de desenvolvimento do Visual Studio.  
  
 Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Exemplo  

 Compile `in.cs`, criando `in.netmodule`:  
  
```console  
csc -target:module in.cs  
```  
  
## <a name="see-also"></a>Confira também

- [-Target (opções do compilador C#)](./target-compiler-option.md)
- [Opções do compilador de C#](./index.md)
