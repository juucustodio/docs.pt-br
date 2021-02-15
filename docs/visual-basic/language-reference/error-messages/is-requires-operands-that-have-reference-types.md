---
description: "Saiba mais sobre: BC30020: ' is ' requer operandos que têm tipos de referência, mas esse operando tem o tipo de valor ' <typename> '"
title: "'Is' requer operandos que tenham tipos de referência, mas este operando tem o tipo de valor '<typename>'"
ms.date: 07/20/2015
f1_keywords:
- bc30020
- vbc30020
helpviewer_keywords:
- BC30020
ms.assetid: 228afebd-1203-4bd3-8d7a-c5c56f3cedc4
ms.openlocfilehash: f05040c6174f4b1edd006d1302f0d94b871d1cd9
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100427538"
---
# <a name="bc30020-is-requires-operands-that-have-reference-types-but-this-operand-has-the-value-type-typename"></a>BC30020: ' is ' requer operandos que têm tipos de referência, mas esse operando tem o tipo de valor ' \<typename> '

O `Is` operador de comparação determina se duas variáveis de objeto se referem à mesma instância. Essa comparação não é definida para tipos de valor.

 **ID do erro:** BC30020

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Use o operador de comparação aritmético apropriado ou o `Like` operador para comparar dois tipos de valor.

## <a name="see-also"></a>Consulte também

- [Operador Is](../operators/is-operator.md)
- [Operador Like](../operators/like-operator.md)
- [Operadores de comparação](../operators/comparison-operators.md)
