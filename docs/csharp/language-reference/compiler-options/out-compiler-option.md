---
description: -out (opções do compilador C#)
title: -out (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /out
helpviewer_keywords:
- /out compiler option [C#]
- out compiler option [C#]
- -out compiler option [C#]
ms.assetid: 70d91d01-7bd2-4aea-ba8b-4e9807e9caa5
ms.openlocfilehash: 409760ee0b147065a2128c62c304fb5d70cfcf42
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193875"
---
# <a name="-out-c-compiler-options"></a>-out (opções do compilador C#)

A opção **-out** especifica o nome do arquivo de saída.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-out:filename  
```  
  
## <a name="arguments"></a>Argumentos  

 `filename`  
 O nome do arquivo de saída criado pelo compilador.  
  
## <a name="remarks"></a>Comentários  

 Na linha de comando, é possível especificar vários arquivos de saída para a compilação. O compilador espera encontrar um ou mais arquivos de código-fonte após a opção **-out**. Em seguida, todos os arquivos de código-fonte serão compilados no arquivo de saída especificado por essa opção **-out**.  
  
 Especifique o nome completo e a extensão do arquivo que você deseja criar.  
  
 Se você não especificar o nome do arquivo de saída:  
  
- Um .exe extrairá seu nome do arquivo de código-fonte que contém o método **principal**.  
  
- Um arquivo .dll ou .netmodule extrairá seu nome do primeiro arquivo de código-fonte.  
  
 Um arquivo de código-fonte usado para compilar um arquivo de saída não pode ser usado na mesma compilação para a compilação de outro arquivo de saída.  
  
 Ao produzir vários arquivos de saída em uma compilação de linha de comando, tenha em mente que somente um dos arquivos de saída pode ser um assembly e que somente o primeiro arquivo de saída especificado (implícita ou explicitamente com **-out**) pode ser o assembly.  
  
 Os módulos produzidos como parte de uma compilação se tornam arquivos associados a qualquer assembly também produzido na compilação. Use [ildasm.exe](../../../framework/tools/ildasm-exe-il-disassembler.md) para exibir o manifesto do assembly para ver os arquivos associados.  
  
 A opção do compilador -out é necessária para que um exe seja o destino de um assembly amigável. Para obter mais informações, consulte [Friend Assemblies](../../../standard/assembly/friend.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto.  
  
2. Clique na página de propriedades do **Aplicativo**.  
  
3. Modifique a propriedade **Nome do Assembly**.  
  
     Para definir essa opção do compilador de maneira programática: <xref:VSLangProj80.ProjectProperties3.OutputFileName%2A> é uma propriedade somente leitura, determinada por uma combinação do tipo de projeto (exe, biblioteca e assim por diante) e o nome do assembly. Será necessário modificar uma ou ambas as propriedades para definir o nome do arquivo de saída.  
  
## <a name="example"></a>Exemplo  

 Compile `t.cs` e crie o arquivo de saída `t.exe`, bem como compile `t2.cs` e crie o arquivo de saída de módulo `mymodule.netmodule`:  
  
```console  
csc t.cs -out:mymodule.netmodule -target:module t2.cs  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Assemblies amigáveis](../../../standard/assembly/friend.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
