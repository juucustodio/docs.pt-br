---
description: Saiba mais sobre:-= operador (Visual Basic)
title: Operador -=
ms.date: 07/20/2015
f1_keywords:
- vb.-=
helpviewer_keywords:
- -= operator [Visual Basic]
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- operator -=
- compound assignment statements [Visual Basic]
ms.assetid: 5ead0c37-ae50-48f7-8435-8e341d81cae1
ms.openlocfilehash: 55574fa56d0ebe02fa5aef1a2711dfb3e5161a9e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795268"
---
# <a name="--operator-visual-basic"></a>Operador -= (Visual Basic)

Subtrai o valor de uma expressão do valor de uma variável ou propriedade e atribui o resultado à variável ou à propriedade.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
variableorproperty -= expression  
```  
  
## <a name="parts"></a>Partes  

 `variableorproperty`  
 Obrigatório. Qualquer variável numérica ou propriedade.  
  
 `expression`  
 Obrigatórios. Qualquer expressão numérica.  
  
## <a name="remarks"></a>Comentários  

 O elemento no lado esquerdo do `-=` operador pode ser uma variável escalar simples, uma propriedade ou um elemento de uma matriz. A variável ou a propriedade não pode ser [ReadOnly](../modifiers/readonly.md).  
  
 Primeiro, o `-=` operador subtrai o valor da expressão (no lado direito do operador) a partir do valor da variável ou da propriedade (no lado esquerdo do operador) do. Em seguida, o operador atribui o resultado dessa operação à variável ou à propriedade.  
  
## <a name="overloading"></a>Sobrecarga  

 O [operador-(Visual Basic)](subtraction-operator.md) pode ser *sobrecarregado*, o que significa que uma classe ou estrutura pode redefinir seu comportamento quando um operando tem o tipo dessa classe ou estrutura. Sobrecarregar o `-` operador afeta o comportamento do `-=` operador. Se o seu código usa `-=` em uma classe ou estrutura que sobrecarrega, certifique-se de `-` entender seu comportamento redefinido. Para obter mais informações, consulte [procedimentos de operador](../../programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa o `-=` operador para subtrair uma `Integer` variável de outra e atribuir o resultado à última variável.  
  
 [!code-vb[VbVbalrOperators#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#11)]  
  
## <a name="see-also"></a>Consulte também

- [Operador - (Visual Basic)](subtraction-operator.md)
- [Operadores de atribuição](assignment-operators.md)
- [Operadores aritméticos](arithmetic-operators.md)
- [Precedência do operador no Visual Basic](operator-precedence.md)
- [Operadores Listados por Funcionalidade](operators-listed-by-functionality.md)
- [Instruções](../../programming-guide/language-features/statements.md)
