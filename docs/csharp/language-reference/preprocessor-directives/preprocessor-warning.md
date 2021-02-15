---
description: '##warning – Referência de C#'
title: '##warning – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#warning'
helpviewer_keywords:
- '#warning directive [C#]'
ms.assetid: e6fb496d-bb8b-4018-baf6-5b60a0c8902b
ms.openlocfilehash: 9ade723bdca17597dcd56240f506e60f2debf6be
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91186413"
---
# <a name="warning-c-reference"></a>#warning (Referência de C#)

`#warning` permite gerar um aviso do compilador [CS1030](../../misc/cs1030.md) de nível um de um local específico no código. Por exemplo:  
  
```csharp
#warning Deprecated code in this method.  
```  
  
## <a name="remarks"></a>Comentários

 Um uso comum de `#warning` é em uma diretiva condicional. Também é possível gerar um erro definido pelo usuário com [#error](./preprocessor-error.md).  
  
## <a name="example"></a>Exemplo  

```csharp
// preprocessor_warning.cs  
// CS1030 expected  
#define DEBUG  
class MainClass
{  
    static void Main()
    {  
#if DEBUG  
#warning DEBUG is defined  
#endif  
    }  
}  
```  

## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
