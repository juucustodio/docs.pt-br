---
description: '#undef – Referência de C#'
title: '#undef – Referência de C#'
ms.date: 06/30/2018
f1_keywords:
- '#undef'
helpviewer_keywords:
- '#undef directive [C#]'
ms.assetid: 686c92d2-7194-4be4-b2f4-80091712d513
ms.openlocfilehash: 7db79be7ea9d8462e09b6ae874bf0ae7d265afe2
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91150551"
---
# <a name="undef-c-reference"></a>#undef (Referência de C#)

`#undef` permite excluir as definições de um símbolo, de modo que, usando o símbolo como a expressão em uma diretiva [#if](./preprocessor-if.md), a expressão será avaliada como `false`.  
  
 Um símbolo pode ser definido com a diretiva [#define](./preprocessor-define.md) ou a opção [-definir](../compiler-options/define-compiler-option.md) compilador. A diretiva `#undef` deve ser exibida no arquivo antes de usar qualquer instrução que também não sejam diretivas.  
  
## <a name="example"></a>Exemplo  

```csharp
// preprocessor_undef.cs  
// compile with: /d:DEBUG  
#undef DEBUG  
using System;  
class MyClass
{  
    static void Main()
    {  
#if DEBUG  
        Console.WriteLine("DEBUG is defined");  
#else  
        Console.WriteLine("DEBUG is not defined");  
#endif  
    }  
}  
```

**DEBUG não está definido**

## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
