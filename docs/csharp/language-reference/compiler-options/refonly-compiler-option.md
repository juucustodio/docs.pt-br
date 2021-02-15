---
description: -refonly (Opções do compilador do C#)
title: -refonly (Opções do compilador do C#)
ms.date: 07/08/2017
f1_keywords:
- /refonly
helpviewer_keywords:
- /refonly compiler option [C#]
- -refonly compiler option [C#]
- refonly compiler option [C#]
ms.openlocfilehash: f9a92462203bedff93a4a711ca8742465b7a561c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89124741"
---
# <a name="-refonly-c-compiler-options"></a>-refonly (Opções do compilador do C#)

A opção **-refonly** indica que um assembly de referência deve ser gerado em vez de um assembly de implementação, como a saída primária. O parâmetro `-refonly` silenciosamente desabilita a geração de PDBs, uma vez que assemblies de referência não podem ser executados. Essa opção corresponde à propriedade de projeto [ProduceOnlyReferenceAssembly](/visualstudio/msbuild/common-msbuild-project-properties) do MSBuild.

## <a name="syntax"></a>Sintaxe

```console
-refonly
```

## <a name="remarks"></a>Comentários

Os assemblies de referência são um tipo especial de assembly que contém apenas a quantidade mínima de metadados necessários para representar a superfície da API pública da biblioteca. Eles incluem declarações para todos os membros que são significativos ao referenciar um assembly em ferramentas de compilação, mas excluem todas as implementações de membro e declarações de membros privados que não têm impacto observável em seu contrato de API. Para obter mais informações, consulte [Reference Assemblies](../../../standard/assembly/reference-assemblies.md) in .net Guide.

As `-refonly` [`-refout`](refout-compiler-option.md) Opções e são mutuamente exclusivas.

## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
