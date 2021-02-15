---
description: '#else – Referência de C#'
title: '#else – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#else'
helpviewer_keywords:
- '#else directive [C#]'
ms.assetid: 6a347322-cfa2-4a86-98f8-ddfa2cb7d4db
ms.openlocfilehash: f0dc8c34672c3e9e5a2207211794fbc8099640c5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168667"
---
# <a name="else-c-reference"></a>#else (Referência de C#)

`#else` permite que você crie uma diretiva condicional composta, para que, caso nenhuma das expressões nas diretivas anteriores [#if](./preprocessor-if.md) ou [#elif](./preprocessor-elif.md) (opcional) seja avaliada como `true`, o compilador avalie todo o código entre `#else` e o próximo `#endif`.  
  
## <a name="remarks"></a>Comentários  

 [#endif](./preprocessor-endif.md) deve ser a próxima diretiva de pré-processador após `#else`. Consulte [#if](./preprocessor-if.md) para obter um exemplo de como usar `#else`.  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
