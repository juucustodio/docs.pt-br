---
description: -filealign (opções do compilador C#)
title: -filealign (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /filealign
helpviewer_keywords:
- /alignment compiler option [C#]
- filealign compiler option [C#]
- -filealign compiler option [C#]
- /sections compiler option [C#]
- alignment compiler option [C#]
- sections compiler option [C#]
- -sections compiler option [C#]
- /filealign compiler option [C#]
- file sharing [C#]
- -alignment compiler option [C#]
- section alignment [C#]
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
ms.openlocfilehash: 4b61217a3d6812ea3ab036f82d49bba05c20629e
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91173237"
---
# <a name="-filealign-c-compiler-options"></a>-filealign (opções do compilador C#)

A opção **-filealign** permite que você especifique o tamanho das seções em seu arquivo de saída.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-filealign:number  
```  
  
## <a name="arguments"></a>Argumentos  

 `number`  
 Um valor que especifica o tamanho das seções no arquivo de saída. Os valores válidos são 512, 1024, 2048, 4096 e 8192. Esses valores estão em bytes.  
  
## <a name="remarks"></a>Comentários  

 Cada seção será alinhada em um limite que é um múltiplo do valor **-filealign**. Não há nenhum padrão fixo. Se **-filealign** não é especificada, o Common Language Runtime escolhe um padrão em tempo de compilação.  
  
 Ao especificar o tamanho da seção, você afeta o tamanho do arquivo de saída. Modificar o tamanho da seção pode ser útil para programas que serão executados em dispositivos menores.  
  
 Use [DUMPBIN](/cpp/build/reference/dumpbin-options) para ver informações sobre as seções em seu arquivo de saída.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto.  
  
2. Clique na página de propriedades **Compilar**.  
  
3. Clique no botão **Avançado** .  
  
4. Modifique a propriedade **Alinhamento de Arquivo**.  
  
 Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>.  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
