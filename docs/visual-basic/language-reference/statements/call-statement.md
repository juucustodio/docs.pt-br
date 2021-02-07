---
description: 'Saiba mais sobre: instrução Call (Visual Basic)'
title: Instrução Call
ms.date: 07/20/2015
f1_keywords:
- vb.Call
helpviewer_keywords:
- procedures [Visual Basic], Call statement
- Call statement [Visual Basic]
- procedures [Visual Basic], calling
ms.assetid: e5b31571-6867-406f-b8e7-a3f9aae4723a
ms.openlocfilehash: 70e6c109621c3710ad9476a952e9c384a142ba3d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99674006"
---
# <a name="call-statement-visual-basic"></a>Instrução Call (Visual Basic)

Transfere o controle para um `Function` `Sub` procedimento, ou DLL (biblioteca de vínculo dinâmico).  
  
## <a name="syntax"></a>Syntax  
  
```vb  
[ Call ] procedureName [ (argumentList) ]  
```  
  
## <a name="parts"></a>Partes  

|||
|---|---|
|`procedureName`|Obrigatório. Nome do procedimento a ser chamado.|
|`argumentList`|Opcional. Lista de variáveis ou expressões que representam argumentos que são passados para o procedimento quando ele é chamado. Vários argumentos são separados por vírgulas. Se você incluir `argumentList` , deverá colocá-lo entre parênteses.|
|||
  
## <a name="remarks"></a>Comentários

 Você pode usar a `Call` palavra-chave ao chamar um procedimento. Para a maioria das chamadas de procedimento, você não precisa usar essa palavra-chave.

 Normalmente, você usa a `Call` palavra-chave quando a expressão chamada não começa com um identificador. O uso da `Call` palavra-chave para outros usos não é recomendado.

 Se o procedimento retornar um valor, a `Call` instrução o descartará.

## <a name="example"></a>Exemplo

 O código a seguir mostra dois exemplos em que a `Call` palavra-chave é necessária para chamar um procedimento. Em ambos os exemplos, a expressão chamada não começa com um identificador.

 [!code-vb[VbVbalrStatements#97](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#97)]  
  
## <a name="see-also"></a>Consulte também

- [Instrução Function](function-statement.md)
- [Instrução Sub](sub-statement.md)
- [Instrução Declare](declare-statement.md)
- [Expressões lambda](../../programming-guide/language-features/procedures/lambda-expressions.md)
