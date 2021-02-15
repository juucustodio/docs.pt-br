---
description: "Saiba mais sobre: BC36635: expressões lambda não são válidas na primeira expressão de uma instrução ' Select Case '"
title: As expressões lambda não são válidas na primeira expressão de uma instrução 'Select Case'
ms.date: 07/20/2015
f1_keywords:
- bc36635
- vbc36635
helpviewer_keywords:
- BC36635
ms.assetid: 74609979-9c03-4864-bbce-f588aa2e0917
ms.openlocfilehash: e0c388db7164f6c9f99ba917109593a796f7b23b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795931"
---
# <a name="bc36635-lambda-expressions-are-not-valid-in-the-first-expression-of-a-select-case-statement"></a>BC36635: expressões lambda não são válidas na primeira expressão de uma instrução ' Select Case '

Você não pode usar uma expressão lambda para a expressão de teste em uma `Select Case` instrução. As definições de expressão lambda retornam funções e a expressão de teste de uma `Select Case` instrução deve ser um tipo de dados elementar.

 O código a seguir causa esse erro:

```vb
' Select Case (Function(arg) arg Is Nothing)
    ' List of the cases.
' End Select
```

 **ID do erro:** BC36635

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Examine seu código para determinar se uma construção condicional diferente, como uma `If...Then...Else` instrução, funcionaria para você.

- Você pode ter pretendido chamar a função, conforme mostrado no código a seguir:

```vb
Dim num? As Integer
Select Case ((Function(arg? As Integer) arg Is Nothing)(num))
    ' List of the cases
End Select
```

## <a name="see-also"></a>Consulte também

- [Expressões lambda](../../programming-guide/language-features/procedures/lambda-expressions.md)
- [Instrução If...Then...Else](../statements/if-then-else-statement.md)
- [Instrução Select...Case](../statements/select-case-statement.md)
