---
description: get – Referência de C#
title: get – Referência de C#
ms.date: 03/10/2017
f1_keywords:
- get_CSharpKeyword
- get
helpviewer_keywords:
- get keyword [C#]
ms.assetid: a52de048-fbe0-41b0-82ec-8e4ac04d3a71
ms.openlocfilehash: 7e13dc3ed6577717c64b4e36000a9e090f7b4751
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89139730"
---
# <a name="get-c-reference"></a>get (Referência de C#)

A palavra-chave `get` define um método do *acessador* em uma propriedade ou um indexador que retorna o valor da propriedade ou o elemento do indexador. Para obter mais informações, consulte [Propriedades](../../programming-guide/classes-and-structs/properties.md), [Propriedades autoimplementadas](../../programming-guide/classes-and-structs/auto-implemented-properties.md) e [Indexadores](../../programming-guide/indexers/index.md).  
  
O exemplo a seguir define um acessador `get` e um acessador `set` para uma propriedade chamada `Seconds`. Ela usa um campo particular chamado `_seconds` para dar suporte ao valor da propriedade.  

 [!code-csharp[get#1](../../../../samples/snippets/csharp/language-reference/keywords/get/get-1.cs)]  
  
Geralmente, o acessador `get` consiste em uma única instrução que retorna um valor, como no exemplo anterior. Começando com o C# 7.0, você pode implementar o acessador `get` como um membro apto para expressão. O exemplo a seguir implementa os acessadores `get` e `set` como membros aptos para expressão.

 [!code-csharp[get#3](../../../../samples/snippets/csharp/language-reference/keywords/get/get-3.cs)]

Para casos simples em que os acessadores `get` e `set` de uma propriedade não realizam nenhuma outra operação, a não ser a configuração ou a recuperação de um valor em um campo de suporte particular, você pode tirar proveito do suporte do compilador do C# para propriedades autoimplementadas. O exemplo a seguir implementa `Hours` como uma propriedade autoimplementada.
  
 [!code-csharp[get#2](../../../../samples/snippets/csharp/language-reference/keywords/get/get-2.cs)]  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Palavras-chave do C#](./index.md)
- [Propriedades](../../programming-guide/classes-and-structs/properties.md)
