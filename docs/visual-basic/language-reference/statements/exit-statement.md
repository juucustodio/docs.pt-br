---
description: 'Saiba mais sobre: instrução Exit (Visual Basic)'
title: Instrução Exit
ms.date: 07/20/2015
f1_keywords:
- vb.Exit
helpviewer_keywords:
- execution [Visual Basic], ending
- files [Visual Basic], closing
- programs [Visual Basic], quitting
- code, exiting
- Exit statement [Visual Basic]
- program termination
- execution [Visual Basic], stopping
ms.assetid: 760bfb32-5c3f-4bdb-a432-9a6001c92db7
ms.openlocfilehash: 54af7fbf908dbad829cf6f08bf442dfe85e35610
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99769112"
---
# <a name="exit-statement-visual-basic"></a>Instrução Exit (Visual Basic)

Sai de um procedimento ou bloco e transfere o controle imediatamente para a instrução após a chamada de procedimento ou a definição de bloco.

## <a name="syntax"></a>Syntax

```vb
Exit { Do | For | Function | Property | Select | Sub | Try | While }
```

## <a name="statements"></a>Instruções

 `Exit Do`  
 Sai imediatamente do `Do` loop no qual ele aparece. A execução continua com a instrução após a `Loop` instrução. `Exit Do` pode ser usado somente dentro de um `Do` loop. Quando usado dentro de `Do` loops aninhados, `Exit Do` sai do loop mais interno e transfere o controle para o próximo nível mais alto de aninhamento.

 `Exit For`  
 Sai imediatamente do `For` loop no qual ele aparece. A execução continua com a instrução após a `Next` instrução. `Exit For` pode ser usado somente dentro de um `For` loop... `Next` ou `For Each` .. `Next` . Quando usado dentro de `For` loops aninhados, `Exit For` sai do loop mais interno e transfere o controle para o próximo nível mais alto de aninhamento.

 `Exit Function`  
 Sai imediatamente do `Function` procedimento no qual ele aparece. A execução continua com a instrução após a instrução que chamou o `Function` procedimento. `Exit Function` pode ser usado somente dentro de um `Function` procedimento.

 Para especificar um valor de retorno, você pode atribuir o valor ao nome da função em uma linha antes da `Exit Function` instrução. Para atribuir o valor de retorno e sair da função em uma instrução, em vez disso, você pode usar a [instrução return](return-statement.md).

 `Exit Property`  
 Sai imediatamente do `Property` procedimento no qual ele aparece. A execução continua com a instrução que chamou o `Property` procedimento, ou seja, com a instrução solicitando ou definindo o valor da propriedade. `Exit Property` pode ser usado somente dentro de um `Get` procedimento ou propriedade `Set` .

 Para especificar um valor de retorno em um `Get` procedimento, você pode atribuir o valor ao nome da função em uma linha antes da `Exit Property` instrução. Para atribuir o valor de retorno e sair do `Get` procedimento em uma instrução, em vez disso, você pode usar a `Return` instrução.

 Em um `Set` procedimento, a `Exit Property` instrução é equivalente à `Return` instrução.

 `Exit Select`  
 Sai imediatamente do `Select Case` bloco no qual ele aparece. A execução continua com a instrução após a `End Select` instrução. `Exit Select` pode ser usado somente dentro de uma `Select Case` instrução.

 `Exit Sub`  
 Sai imediatamente do `Sub` procedimento no qual ele aparece. A execução continua com a instrução após a instrução que chamou o `Sub` procedimento. `Exit Sub` pode ser usado somente dentro de um `Sub` procedimento.

 Em um `Sub` procedimento, a `Exit Sub` instrução é equivalente à `Return` instrução.

 `Exit Try`  
 Sai imediatamente do `Try` bloco ou `Catch` em que ele aparece. A execução continua com o `Finally` bloco se houver um, ou com a instrução após a `End Try` instrução, caso contrário. `Exit Try` pode ser usado somente dentro de `Try` um `Catch` bloco ou e não dentro de um `Finally` bloco.

 `Exit While`  
 Sai imediatamente do `While` loop no qual ele aparece. A execução continua com a instrução após a `End While` instrução. `Exit While` pode ser usado somente dentro de um `While` loop. Quando usado em `While` loops aninhados, o `Exit While` transfere o controle para o loop que é um nível aninhado acima do loop onde `Exit While` ocorre.

## <a name="remarks"></a>Comentários

Não confunda `Exit` instruções com `End` instruções. `Exit` não define o fim de uma instrução.

## <a name="example"></a>Exemplo

No exemplo a seguir, a condição de loop para o loop quando a `index` variável é maior que 100. No `If` entanto, a instrução no loop faz com que a `Exit Do` instrução pare o loop quando a variável de índice for maior que 10.

[!code-vb[VbVbalrStatements#133](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#133)]

## <a name="example"></a>Exemplo

O exemplo a seguir atribui o valor de retorno ao nome da função `myFunction` e, em seguida, usa `Exit Function` para retornar da função:

[!code-vb[VbVbalrStatements#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#23)]

## <a name="example"></a>Exemplo

O exemplo a seguir usa a [instrução return](return-statement.md) para atribuir o valor de retorno e sair da função:

[!code-vb[VbVbalrStatements#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#24)]

## <a name="see-also"></a>Consulte também

- [Instrução Continue](continue-statement.md)
- [Instrução Do...Loop](do-loop-statement.md)
- [Instrução End](end-statement.md)
- [Instrução For Each...Next](for-each-next-statement.md)
- [Instrução For...Next](for-next-statement.md)
- [Instrução Function](function-statement.md)
- [Instrução Return](return-statement.md)
- [Instrução Stop](stop-statement.md)
- [Instrução Sub](sub-statement.md)
- [Instrução Try...Catch...Finally](try-catch-finally-statement.md)
