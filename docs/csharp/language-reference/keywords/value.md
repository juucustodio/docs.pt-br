---
description: Palavra-chave contextual value – Referência de C#
title: Palavra-chave contextual value – Referência de C#
ms.date: 07/20/2015
f1_keywords:
- value_CSharpKeyword
helpviewer_keywords:
- value keyword [C#]
ms.assetid: c99d6468-687f-4a46-89b4-a95e1b00bf6d
ms.openlocfilehash: ad2eb6f12d8c295dc5203994d6c570cd2377e3ee
ms.sourcegitcommit: 43ed174f085840ca18a791dc89fe833174da766d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828910"
---
# <a name="value-c-reference"></a>value (Referência de C#)

A palavra-chave contextual `value` é usada no `set` acessador em declarações de [Propriedade](../../programming-guide/classes-and-structs/properties.md) e [indexador](../../programming-guide/indexers/index.md) . É semelhante a um parâmetro de entrada de um método. A palavra `value` faz referência ao valor que o código do cliente está tentando atribuir à propriedade ou ao indexador. No exemplo a seguir, `MyDerivedClass` tem uma propriedade chamada `Name` que usa o parâmetro `value` para atribuir uma nova cadeia de caracteres ao campo de suporte `name`. Do ponto de vista do código cliente, a operação é gravada como uma atribuição simples.

[!code-csharp[csrefKeywordsModifiers#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#26)]

Para obter mais informações, consulte os artigos sobre [Propriedades](../../programming-guide/classes-and-structs/properties.md) e [indexadores](../../programming-guide/indexers/index.md) .

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Palavras-chave do C#](index.md)
