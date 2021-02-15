---
description: "Saiba mais sobre: BC32128: o operando ' IsNot ' do tipo ' TypeName ' só pode ser comparado a ' Nothing ', pois ' TypeName ' é um tipo anulável"
title: O operando 'IsNot' do tipo 'typename' só pode ser comparado a 'Nothing', porque 'typename' é um tipo que permite valor nulo
ms.date: 07/20/2015
f1_keywords:
- bc32128
- vbc32128
helpviewer_keywords:
- BC32128
ms.assetid: 1155b23a-ad75-4bab-b9da-73f35c767a36
ms.openlocfilehash: 732c8bee2ae352824c7d50bba8b2b35598d6f53b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795983"
---
# <a name="bc32128-isnot-operand-of-type-typename-can-only-be-compared-to-nothing-because-typename-is-a-nullable-type"></a>BC32128: o operando ' IsNot ' do tipo ' TypeName ' só pode ser comparado a ' Nothing ', pois ' TypeName ' é um tipo anulável

Uma variável declarada como um tipo de valor anulável foi comparada a uma expressão diferente de `Nothing` usar o `IsNot` operador.

**ID do erro:** BC32128

## <a name="to-correct-this-error"></a>Para corrigir este erro

Para comparar um tipo anulável a uma expressão que não seja `Nothing` usando o `IsNot` operador, chame o `GetType` método no tipo anulável e compare o resultado com a expressão, conforme mostrado no exemplo a seguir.

```vb
Dim number? As Integer = 5

If number IsNot Nothing Then
  If number.GetType() IsNot Type.GetType("System.Int32") Then

  End If
End If
```

## <a name="see-also"></a>Consulte também

- [Tipos de valor anulável](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [Operador IsNot](../operators/isnot-operator.md)
