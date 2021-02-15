---
description: Saiba mais sobre:-refout (Visual Basic)
title: -refout
ms.date: 03/16/2018
f1_keywords:
- /refout
helpviewer_keywords:
- refout compiler option [Visual Basic]
- /refout compiler option [Visual Basic]
- -refout compiler option [Visual Basic]
ms.openlocfilehash: 2760f7e60d950aaff90becad843824a2e2b4379f
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100474116"
---
# <a name="-refout-visual-basic"></a>-refout (Visual Basic)

A opção **-refout** especifica um caminho de arquivo em que o assembly de referência deve ser gerado.

[!INCLUDE[compiler-options](~/includes/compiler-options.md)]

## <a name="syntax"></a>Sintaxe

```console
-refout:filepath
```

## <a name="arguments"></a>Argumentos

`filepath`  
O caminho e o nome do arquivo do assembly de referência. Em geral, ele deve estar em uma subpasta do assembly primário. A convenção recomendada (usada pelo MSBuild) é colocar o assembly de referência em uma subpasta "ref/" em relação ao assembly principal. Todas as pastas no `filepath` devem existir; o compilador não as cria.

## <a name="remarks"></a>Comentários

Visual Basic dá suporte à `-refout` opção a partir da versão 15,3.

Os assemblies de referência são um tipo especial de assembly que contém apenas a quantidade mínima de metadados necessários para representar a superfície da API pública da biblioteca. Eles incluem declarações para todos os membros que são significativos ao referenciar um assembly em ferramentas de compilação, mas excluem todas as implementações de membro e declarações de membros privados que não têm impacto observável em seu contrato de API. Para obter mais informações, consulte [Reference Assemblies](../../../standard/assembly/reference-assemblies.md) in .net Guide.

As `-refout` [`-refonly`](refonly-compiler-option.md) Opções e são mutuamente exclusivas.

## <a name="see-also"></a>Consulte também

- [-refonly](refonly-compiler-option.md)
- [Compilador de linha de comando do Visual Basic](index.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
