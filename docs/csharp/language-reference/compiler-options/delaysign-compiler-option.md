---
description: -delaysign (opções do compilador C#)
title: -delaysign (opções do compilador C#)
ms.date: 05/15/2018
f1_keywords:
- /delaysign
helpviewer_keywords:
- -delaysign compiler option [C#]
- delaysign compiler option [C#]
- /delaysign compiler option [C#]
ms.assetid: bcb058eb-2933-4e7f-b356-5c941db4de75
ms.openlocfilehash: 5512ebeca4672f5d69852ab07c3f3fa40c305327
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89125833"
---
# <a name="-delaysign-c-compiler-options"></a>-delaysign (opções do compilador C#)

Essa opção faz com que o compilador reserve espaço no arquivo de saída para que uma assinatura digital possa ser adicionada mais tarde.

## <a name="syntax"></a>Sintaxe

```console
-delaysign[ + | - ]
```

## <a name="arguments"></a>Argumentos

`+` &#124; `-`

Use **-delaysign-** se você quiser um assembly totalmente assinado. Use **-delaysign+** se você apenas desejar colocar a chave pública no assembly. O padrão é **-delaysign-**.

## <a name="remarks"></a>Comentários

A opção **-delaysign** não tem nenhum efeito, a menos que seja usada com [-keyfile](./keyfile-compiler-option.md) ou [-keycontainer](./keycontainer-compiler-option.md).

As opções **-delaysign** e **-publicsign** são mutuamente exclusivas.

Quando você solicita um assembly totalmente assinado, o compilador usa o hash no arquivo que contém o manifesto (metadados de assembly) e sinaliza esse hash com a chave particular. Essa operação cria uma assinatura digital que é armazenada no arquivo que contém o manifesto. Quando um assembly é assinado com atraso, o compilador não calcula e armazena a assinatura, mas reserva o espaço no arquivo, de forma que a assinatura possa ser adicionada depois.

Por exemplo, o uso de **-delaysign+** permite que um testador coloque o assembly no cache global. Após o teste, é possível assinar completamente o assembly, colocando a chave particular no assembly com o utilitário [Assembly Linker](../../../framework/tools/al-exe-assembly-linker.md).

Para obter mais informações, consulte [Criando e usando assemblies de nomes fortes](../../../standard/assembly/create-use-strong-named.md) e [Atraso na Assinatura de um Assembly](../../../standard/assembly/delay-sign.md).

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio

1. Abra a página **Propriedades** do projeto.
1. Modifique a propriedade **Apenas adiar a assinatura**.

Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.

## <a name="see-also"></a>Confira também

- [Opção -publicsign do C#](publicsign-compiler-option.md)
- [Opções do compilador de C#](index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
