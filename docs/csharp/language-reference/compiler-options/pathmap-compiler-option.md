---
description: -pathmap (opções do compilador C#)
title: -pathmap (opções do compilador C#)
ms.date: 05/16/2018
f1_keywords:
- /pathmap
helpviewer_keywords:
- -pathmap compiler option [C#]
- pathmap compiler option [C#]
- /pathmap compiler option [C#]
ms.openlocfilehash: 707a37c6946cfcaf429552f0aeece6b87f3ad71d
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89125001"
---
# <a name="-pathmap-c-compiler-options"></a>-pathmap (opções do compilador C#)

A opção do compilador **-pathmap** especifica como mapear caminhos físicos para os nomes de caminho de origem emitidos pelo compilador.

## <a name="syntax"></a>Sintaxe

```console
-pathmap:path1=sourcePath1,path2=sourcePath2
```

## <a name="arguments"></a>Argumentos

 `path1` O caminho completo para os arquivos de origem no ambiente atual

 `sourcePath1` O caminho de origem substituído por `path1` em arquivos de saída.

Para especificar vários caminhos de origem mapeados, separe-os com uma vírgula.

## <a name="remarks"></a>Comentários

O compilador grava o caminho de origem em sua saída pelos seguintes motivos:

1. O caminho de origem é substituído por um argumento quando o <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> é aplicado a um parâmetro opcional.
1. O caminho de origem é inserido em um arquivo PDB.
1. O caminho do arquivo PDB é inserido em um arquivo PE (executável portátil).

Essa opção mapeia cada caminho físico no computador em que o compilador é executado para um caminho correspondente que deve ser gravado nos arquivos de saída.

## <a name="example"></a>Exemplo

Compilar `t.cs` no diretório **C:\\work\\tests** e mapear esse diretório para **\publish** na saída:

```console
csc -pathmap:C:\work\tests=\publish t.cs
```

## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
