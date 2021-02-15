---
description: 'Saiba mais sobre: substituições (Visual Basic)'
title: Substituições
ms.date: 07/20/2015
f1_keywords:
- Overrides
- vb.Overrides
helpviewer_keywords:
- properties [Visual Basic], redefining
- procedures [Visual Basic], overriding
- procedures [Visual Basic], redefining
- overriding
- Overrides keyword [Visual Basic]
- overriding, Overrides keyword
- properties [Visual Basic], overriding
ms.assetid: 9f5e6144-ce10-465e-842b-1a8f8760af90
ms.openlocfilehash: d118bf4e366ff8f84806586dfc3977612ed6eff4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99730441"
---
# <a name="overrides-visual-basic"></a>Substituições (Visual Basic)

Especifica que uma propriedade ou procedimento substitui uma propriedade nomeada de forma idêntica ou procedimento herdado de uma classe base.

## <a name="rules"></a>Regras

- **Contexto de declaração.** Você pode usar `Overrides` somente em uma instrução de declaração de propriedade ou de procedimento.

- **Modificadores combinados.** Você não pode especificar `Overrides` juntos com `Shadows` ou `Shared` na mesma declaração. Como um elemento de substituição é implicitamente substituível, você não pode combinar `Overridable` com `Overrides` .

- **Assinaturas correspondentes.** A assinatura dessa declaração deve corresponder exatamente à *assinatura* da propriedade ou do procedimento que ela substitui. Isso significa que as listas de parâmetros devem ter o mesmo número de parâmetros, na mesma ordem, com os mesmos tipos de dados.

  Além da assinatura, a declaração de substituição também deve corresponder exatamente ao seguinte:

  - O nível de acesso

  - O tipo de retorno, se houver

- **Assinaturas genéricas.** Para um procedimento genérico, a assinatura inclui o número de parâmetros de tipo. Portanto, a declaração de substituição também deve corresponder à versão da classe base nesse aspecto.

- **Correspondência adicional.** Além de corresponder à assinatura da versão da classe base, essa declaração também deve corresponder aos seguintes aspectos:

  - Modificador de nível de acesso (como [público](public.md))

  - Mecanismo de passagem de cada parâmetro ([ByVal](byval.md) ou [ByRef](byref.md))

  - Listas de restrição em cada parâmetro de tipo de um procedimento genérico

- **Sombreamento e substituição.** Sombreamento e substituição redefinem um elemento herdado, mas há diferenças significativas entre as duas abordagens. Para obter mais informações, consulte [sombreamento em Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md).

Se você usar `Overrides` o, o compilador adicionará implicitamente `Overloads` para que suas APIs de biblioteca trabalhem com o C# mais facilmente.

O `Overrides` modificador pode ser usado nesses contextos:

- [Instrução Function](../statements/function-statement.md)

- [Instrução Property](../statements/property-statement.md)

- [Instrução Sub](../statements/sub-statement.md)

## <a name="see-also"></a>Consulte também

- [MustOverride](mustoverride.md)
- [NotOverridable](notoverridable.md)
- [Substituível](overridable.md)
- [Palavras-chave](../keywords/index.md)
- [Sombreamento no Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md)
- [Tipos genéricos no Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [Lista de Tipos](../statements/type-list.md)
