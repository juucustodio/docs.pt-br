---
description: '##pragma warning – Referência de C#'
title: '##pragma warning – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#pragma warning'
helpviewer_keywords:
- '#pragma warning [C#]'
ms.assetid: 723493d5-9753-4cec-babb-54e2b8eb36b6
ms.openlocfilehash: 16582a74bd34f2c0d89950280f1d5fde25435eea
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99215986"
---
# <a name="pragma-warning-c-reference"></a>#pragma warning (Referência de C#)

O `#pragma warning` pode habilitar ou desabilitar determinados avisos.

## <a name="syntax"></a>Sintaxe

```csharp
#pragma warning disable warning-list
#pragma warning restore warning-list
```

## <a name="parameters"></a>Parâmetros

 `warning-list` Uma lista separada por vírgulas de números de aviso. O prefixo "CS" é opcional.

 Quando não houver números de aviso especificados, o `disable` desabilita todos os avisos e o `restore` habilita todos os avisos.

> [!NOTE]
> Para localizar números de aviso no Visual Studio, compile o projeto e, em seguida, procure os números de aviso na janela de **Saída**.

## <a name="example"></a>Exemplo

```csharp
// pragma_warning.cs
using System;

#pragma warning disable 414, CS3021
[CLSCompliant(false)]
public class C
{
    int i = 1;
    static void Main()
    {
    }
}
#pragma warning restore CS3021
[CLSCompliant(false)]  // CS3021
public class D
{
    int i = 1;
    public static void F()
    {
    }
}
```

## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
- [Erros do compilador C#](../compiler-messages/index.md)
- [Como suprimir avisos de análise de código](../../../fundamentals/code-analysis/suppress-warnings.md)
