---
description: -debug (opções do compilador C#)
title: -debug (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /debug
helpviewer_keywords:
- debug compiler option [C#]
- -debug compiler option [C#]
- /debug compiler option [C#]
ms.assetid: e2b48c07-01bc-45cc-a52c-92e9085eb969
ms.openlocfilehash: 77aa9bf0fc0911f441d00403d773ee5ae03ae99b
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91173289"
---
# <a name="-debug-c-compiler-options"></a>-debug (opções do compilador C#)

A opção **-debug** faz o compilador gerar informações de depuração e colocá-las nos arquivos de saída.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-debug[+ | -]  
-debug:{full | pdbonly}  
```  
  
## <a name="arguments"></a>Argumentos  

 `+` &#124; `-`  
 Especificar `+` ou apenas **-debug** faz o compilador gerar informações de depuração e colocá-las em um de banco de dados de programa (arquivo .pdb). Especificar `-`, que será aplicado se **-debug** não for especificado, faz com que nenhuma informação de depuração seja criada.  
  
 `full` &#124; `pdbonly`  
 Especifica o tipo de informações de depuração geradas pelo compilador. O argumento completo, que será aplicado se **-debug:pdbonly** não for especificado, permite anexar um depurador ao programa em execução. Especificar pdbonly habilita a depuração do código-fonte quando o programa é iniciado no depurador, mas exibirá somente o assembler quando o programa em execução for anexado ao depurador.  
  
## <a name="remarks"></a>Comentários  

 Use essa opção para criar builds de depuração. Caso **-debug**, **-debug+** ou **-debug:full** não sejam especificados, não será possível depurar o arquivo de saída do programa.  
  
 Caso **-debug:full** seja usado, lembre-se de que isso influenciará a velocidade e o tamanho do código otimizado JIT e haverá um pequeno impacto na qualidade do código com **-debug:full**. Recomenda-se **-debug:pdbonly** ou nenhum PDB para gerar código de versão.  
  
> [!NOTE]
> Uma diferença entre **-debug:pdbonly** e **-debug:full** é que, com **-debug:full**, o compilador emite uma <xref:System.Diagnostics.DebuggableAttribute>, que é usada para avisar ao compilador JIT que as informações de depuração estão disponíveis. Portanto, haverá um erro se o código contiver <xref:System.Diagnostics.DebuggableAttribute> definido como false, caso **-debug:full** seja usado.  
  
 Para obter informações sobre como configurar o desempenho de depuração de um aplicativo, consulte [Facilitando a Depuração de uma Imagem](../../../framework/debug-trace-profile/making-an-image-easier-to-debug.md).  
  
 Para alterar o local do arquivo. pdb, consulte [-PDB (opções do compilador C#)](./pdb-compiler-option.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto.  
  
2. Clique na página de propriedades **Compilar**.  
  
3. Clique no botão **Avançado** .  
  
4. Modifique a propriedade **Informações de Depuração**.  
  
 Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DebugSymbols%2A>.  
  
## <a name="example"></a>Exemplo  

 Coloque as informações de depuração no arquivo de saída `app.pdb`:  
  
```console  
csc -debug -pdb:app.pdb test.cs  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
