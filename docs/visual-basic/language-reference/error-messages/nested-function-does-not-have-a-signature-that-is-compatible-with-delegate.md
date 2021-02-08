---
description: "Saiba mais sobre: BC36532: a função aninhada não tem uma assinatura compatível com o delegado '<delegatename>"
title: A função aninhada não tem uma assinatura que seja compatível com o delegado '<delegatename>'
ms.date: 07/20/2015
f1_keywords:
- vbc36532
- bc36532
helpviewer_keywords:
- BC36532
ms.assetid: 493f292c-d81e-40ef-8b47-61f020571829
ms.openlocfilehash: 2220faacdac065718a302ef7b086f99bf1e16cef
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795658"
---
# <a name="bc36532-nested-function-does-not-have-a-signature-that-is-compatible-with-delegate-delegatename"></a>BC36532: a função aninhada não tem uma assinatura compatível com o delegado ' \<delegatename> '

Uma expressão lambda foi atribuída a um delegado que tem uma assinatura incompatível. Por exemplo, no código a seguir, o delegado `Del` tem dois parâmetros inteiros.

```vb
Delegate Function Del(ByVal p As Integer, ByVal q As Integer) As Integer
```

O erro será gerado se uma expressão lambda com um argumento for declarada como tipo `Del` :

```vb
' Neither of these is valid.
' Dim lambda1 As Del = Function(n As Integer) n + 1
' Dim lambda2 As Del = Function(n) n + 1
```

**ID do erro:** BC36532

## <a name="to-correct-this-error"></a>Para corrigir este erro

Ajuste a definição de delegado ou a expressão lambda atribuída para que as assinaturas sejam compatíveis.

## <a name="see-also"></a>Consulte também

- [Conversão de delegado reduzida](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [Expressões lambda](../../programming-guide/language-features/procedures/lambda-expressions.md)
