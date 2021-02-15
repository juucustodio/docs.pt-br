---
description: Modificador override – Referência de C#
title: Modificador override – Referência de C#
ms.date: 10/22/2020
f1_keywords:
- override
- override_CSharpKeyword
helpviewer_keywords:
- override keyword [C#]
ms.assetid: dd1907a8-acf8-46d3-80b9-c2ca4febada8
ms.openlocfilehash: 618200183348e68a4600adb9592a635f61f6a875
ms.sourcegitcommit: 98d20cb038669dca4a195eb39af37d22ea9d008e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92434877"
---
# <a name="override-c-reference"></a>Override (referência C#)

O modificador `override` é necessário para estender ou modificar a implementação abstrata ou virtual de um método, propriedade, indexador ou evento herdado.

No exemplo a seguir, a `Square` classe deve fornecer uma implementação substituída de `GetArea` porque `GetArea` é herdada da `Shape` classe abstrata:

[!code-csharp[csrefKeywordsModifiers#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#1)]

Um `override` método fornece uma nova implementação do método herdado de uma classe base. O método que é substituído por uma declaração `override` é conhecido como o método base substituído. Um `override` método deve ter a mesma assinatura que o método base substituído. A partir do C# 9,0, os `override` métodos dão suporte a tipos de retorno covariantes. Em particular, o tipo de retorno de um `override` método pode derivar do tipo de retorno do método base correspondente. No C# 8,0 e anteriores, os tipos de retorno de um `override` método e o método base substituído devem ser iguais.

Você não pode substituir um método não virtual ou estático. O método base substituído deve ser `virtual`, `abstract` ou `override`.

Uma declaração `override` não pode alterar a acessibilidade do método `virtual`. O método `override` e o método `virtual` devem ter o mesmo [modificador de nível de acesso](access-modifiers.md).

Não é possível usar os modificadores `new`, `static` ou `virtual` para modificar um método `override`.

Uma declaração de propriedade de substituição deve especificar exatamente o mesmo modificador de acesso, tipo e nome que a propriedade herdada. A partir do C# 9,0, as propriedades de substituição somente leitura dão suporte a tipos de retorno covariantes. A propriedade substituída deve ser `virtual` , `abstract` ou `override` .

Para obter mais informações sobre como usar a `override` palavra-chave, consulte [controle de versão com a substituição e novas palavras-chave](../../programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md) e [saber quando usar substituições e novas palavras-chave](../../programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md). Para obter informações sobre herança, consulte [Herança](../../programming-guide/classes-and-structs/inheritance.md).

## <a name="example"></a>Exemplo

Este exemplo define uma classe base chamada `Employee` e uma classe derivada chamada `SalesEmployee`. A classe `SalesEmployee` inclui um campo extra, `salesbonus`, e substitui o método `CalculatePay` para levar isso em consideração.

[!code-csharp[csrefKeywordsModifiers#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#9)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, consulte a seção [métodos de substituição](~/_csharplang/spec/classes.md#override-methods) da [especificação da linguagem C#](~/_csharplang/spec/introduction.md).

Para obter mais informações sobre tipos de retorno covariantes, consulte a [Nota de proposta de recurso](~/_csharplang/proposals/csharp-9.0/covariant-returns.md).

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Herança](../../programming-guide/classes-and-structs/inheritance.md)
- [Palavras-chave do C#](index.md)
- [Modificadores](index.md)
- [resume](abstract.md)
- [virtual](virtual.md)
- [novo (modificador)](new-modifier.md)
- [Polimorfismo](../../programming-guide/classes-and-structs/polymorphism.md)
