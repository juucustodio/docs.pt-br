---
description: -keycontainer (opções do compilador C#)
title: -keycontainer (opções do compilador C#)
ms.date: 05/16/2018
f1_keywords:
- /keycontainer
helpviewer_keywords:
- /keycontainer compiler option [C#]
- keycontainer compiler option [C#]
- -keycontainer compiler option [C#]
ms.assetid: b3982b6d-2382-4f7e-bebd-ce98eaa30763
ms.openlocfilehash: 93ee5cd755a4fd6918d2a5825b63151a201a8f6a
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91152462"
---
# <a name="-keycontainer-c-compiler-options"></a>-keycontainer (opções do compilador C#)

Especifica o nome do contêiner da chave de criptografia.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-keycontainer:string  
```  
  
## <a name="arguments"></a>Argumentos  

 `string`  
 O nome do contêiner de chave de nome forte.  
  
## <a name="remarks"></a>Comentários  

 Quando a opção **-keycontainer** for usada, o compilador criará um componente compartilhável. O compilador insere uma chave pública do contêiner especificado no manifesto do assembly e assina o assembly final com a chave privada. Para gerar um arquivo de chave, digite `sn -k file` na linha de comando. `sn -i` instala o par de chaves no contêiner. Não há suporte para essa opção quando o compilador é executado no CoreCLR. Para assinar um assembly ao compilar no CoreCLR, use a opção [-keyfile](keyfile-compiler-option.md).
  
 Se você compilar com [-target:module](./target-module-compiler-option.md), o nome do arquivo de chave será mantido no módulo e incorporado no assembly quando você compilar esse módulo em um assembly com [-addmodule](./addmodule-compiler-option.md).  
  
 Também é possível especificar essa opção como um atributo personalizado (<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=nameWithType>) no código-fonte de qualquer módulo MSIL (Microsoft Intermediate Language).  
  
 Também é possível passar suas informações de criptografia para o compilador com [-keyfile](./keyfile-compiler-option.md). Use [-delaysign](./delaysign-compiler-option.md) se você quiser que a chave pública seja adicionada ao manifesto do assembly, mas deseja atrasar a assinatura do assembly até que ela seja testada.  
  
 Para obter mais informações, consulte [Criando e usando assemblies de nomes fortes](../../../standard/assembly/create-use-strong-named.md) e [Atraso na Assinatura de um Assembly](../../../standard/assembly/delay-sign.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Essa opção do compilador não está disponível no ambiente de desenvolvimento do Visual Studio.  
  
 Você pode acessar programaticamente essa opção do compilador com <xref:VSLangProj.ProjectProperties.AssemblyKeyContainerName%2A>.  
  
## <a name="see-also"></a>Confira também

- [Opção -keyfile do compilador C#](keyfile-compiler-option.md)
- [Opções do compilador de C#](index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
