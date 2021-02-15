---
description: -nostdlib (opções do compilador C#)
title: -nostdlib (opções do compilador C#)
ms.date: 12/20/2019
f1_keywords:
- /nostdlib
helpviewer_keywords:
- nostdlib compiler option [C#]
- -nostdlib compiler option [C#]
- /nostdlib compiler option [C#]
ms.assetid: ec197989-fa49-4725-a455-e06b551eb65f
ms.openlocfilehash: 214918b32f1f1276eb936e66daba3d372a1e9228
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89125092"
---
# <a name="-nostdlib-c-compiler-options"></a>-nostdlib (opções do compilador C#)

**-nostdlib** impede a importação de mscorlib.dll, que define todo o namespace System.

## <a name="syntax"></a>Sintaxe

```console
-nostdlib[+ | -]
```

## <a name="remarks"></a>Comentários

Use essa opção se desejar definir ou criar seus próprios objetos e namespace System.

Se você não especificar **-nostdlib**, o mscorlib.dll será importado no programa (o mesmo que especificar **-nostdlib-**). Especificar **-nostdlib** é o mesmo que especificar **-nostdlib+**.

### <a name="to-set-this-compiler-option-in-visual-studio"></a>Para definir essa opção do compilador no Visual Studio

> [!NOTE]
> As instruções a seguir se aplicam apenas ao Visual Studio 2015 (e a versões anteriores). A propriedade não **referenciar mscorlib.dll** Build não existe em versões mais recentes do Visual Studio.

1. Abra a página **Propriedades** do projeto.

2. Clique na página de propriedades **Compilar**.

3. Clique no botão **Avançado** .

4. Modifique a propriedade **Não referenciar mscorlib.dll**.

### <a name="to-set-this-compiler-option-programmatically"></a>Para definir essa opção do compilador via programação

Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.CSharpProjectConfigurationProperties3.NoStdLib%2A>.

## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
