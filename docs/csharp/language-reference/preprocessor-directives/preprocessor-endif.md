---
description: '#endif – Referência de C#'
title: '#endif – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#endif'
helpviewer_keywords:
- '#endif directive [C#]'
ms.assetid: 6a5fca55-5aee-441f-86f6-1c99fbe9ec05
ms.openlocfilehash: 0ccc00ceab2aa67c77140e3ef09907ba260d7e9b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168628"
---
# <a name="endif-c-reference"></a>#endif (Referência de C#)

O `#endif` especifica o final de uma diretiva condicional, que começou com a diretiva [#if](./preprocessor-if.md). Por exemplo,  
  
```csharp
#define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
## <a name="remarks"></a>Comentários  

 Uma diretiva condicional, começando com uma diretiva `#if`, deve ser encerrada explicitamente com uma diretiva `#endif`. Consulte [#if](./preprocessor-if.md) para obter um exemplo de como usar `#endif`.  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
