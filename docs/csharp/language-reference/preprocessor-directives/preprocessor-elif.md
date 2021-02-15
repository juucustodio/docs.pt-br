---
description: '#elif – Referência de C#'
title: '#elif – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#elif'
helpviewer_keywords:
- '#elif directive [C#]'
ms.assetid: 731d78df-08e0-4d51-b8c8-f193c27de13f
ms.openlocfilehash: 383c143792a39bb3abcd255804360ad5e2f8ef74
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168693"
---
# <a name="elif-c-reference"></a>#elif (Referência de C#)

O `#elif` permite criar uma diretiva condicional composta. A expressão `#elif` será avaliada se nenhum dos [#if](./preprocessor-if.md) anteriores nem nenhuma diretiva `#elif`, opcional, anterior avaliar expressões para `true`. Se uma expressão `#elif` for avaliada como `true`, o compilador avalia todo o código entre o `#elif` e a próxima diretiva condicional. Por exemplo:  
  
```csharp
#define VC7  
//...  
#if debug  
    Console.WriteLine("Debug build");  
#elif VC7  
    Console.WriteLine("Visual Studio 7");  
#endif  
```  
  
 É possível usar os operadores `==` (igualdade), `!=` (desigualdade), `&&` (e) e `||` (ou), para avaliar vários símbolos. Também é possível agrupar os símbolos e operadores com parênteses.  
  
## <a name="remarks"></a>Comentários  

 `#elif` é equivalente a usar:  
  
```csharp
#else  
#if  
```  
  
 Usar `#elif` é mais simples, porque cada `#if` requer um [#endif](./preprocessor-endif.md), enquanto um `#elif` pode ser usado sem um `#endif` de correspondência.  
  
 Consulte [#if](./preprocessor-if.md) para obter um exemplo de como usar `#elif`.  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
