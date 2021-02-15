---
description: Saiba mais sobre:-Quiet
title: -quiet
ms.date: 07/20/2015
f1_keywords:
- -quiet
- quiet
helpviewer_keywords:
- -quiet compiler option [Visual Basic]
- /quiet compiler option [Visual Basic]
- quiet compiler option [Visual Basic]
ms.assetid: 5d77fa23-4c50-4708-8535-649912b098e8
ms.openlocfilehash: 23e1b6472e80ac6ca2ecea5c4390b43722ccebb6
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100432722"
---
# <a name="-quiet"></a>-quiet

Impede que o compilador exiba código para erros e avisos relacionados à sintaxe.

## <a name="syntax"></a>Sintaxe

```console
-quiet
```

## <a name="remarks"></a>Comentários

Por padrão, `-quiet` não está em vigor. Quando o compilador relata um erro ou aviso relacionado à sintaxe, ele também gera a linha do código-fonte. Para aplicativos que analisam a saída do compilador, pode ser mais conveniente para o compilador gerar somente o texto do diagnóstico.

No exemplo a seguir, `Module1` gera um erro que inclui o código-fonte quando compilado sem `-quiet` .

```vb
Module Module1
    Sub Main()
        x()
    End Sub
End Module
```

Saída:

```console
C:\projects\vb2.vb(3) : error BC30451: 'x' is not declared. It may be inaccessible due to its protection level.

        x()
        ~
```

Compilado com `-quiet` , o compilador gera apenas o seguinte:

```console
E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.
```

> [!NOTE]
> A `-quiet` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ela está disponível somente durante a compilação na linha de comando.

## <a name="example"></a>Exemplo

O código a seguir compila `T2.vb` e não exibe código para diagnósticos de compilador relacionados à sintaxe:

```console
vbc -quiet t2.vb
```

## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
