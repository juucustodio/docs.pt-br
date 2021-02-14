---
description: 'Saiba mais sobre: como definir um operador (Visual Basic)'
title: Como definir um operador
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- operators [Visual Basic], defining
- procedures [Visual Basic], operator
- Visual Basic code, operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- operator procedures [Visual Basic], about operator procedures
- return values [Visual Basic], Operator procedures
- operator overloading
ms.assetid: d4b0e253-092a-4e6e-9fe2-01f562140a29
ms.openlocfilehash: ead96a302426c6f5b1667bb030aab56afe3284c8
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100462705"
---
# <a name="how-to-define-an-operator-visual-basic"></a>Como definir um operador (Visual Basic)

Se você tiver definido uma classe ou estrutura, poderá definir o comportamento de um operador padrão (como `*` , `<>` ou `And` ) quando um ou ambos os operandos forem do tipo de sua classe ou estrutura.  
  
 Defina o operador padrão como um procedimento de operador dentro da classe ou estrutura. Todos os procedimentos de operador devem ser `Public` `Shared` .  
  
 A definição de um operador em uma classe ou estrutura também é chamada de *sobrecarga* do operador.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir define o `+` operador para uma estrutura chamada `height` . A estrutura usa alturas medidas em pés e polegadas. Uma *polegada* é de 2,54 centímetros e um *pé* é de 12 polegadas. Para garantir valores normalizados (polegadas < 12,0), o construtor executa aritmética de *módulo* 12. O `+` operador usa o construtor para gerar valores normalizados.  
  
 [!code-vb[VbVbcnProcedures#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#25)]  
  
 Você pode testar a estrutura `height` com o código a seguir.  
  
 [!code-vb[VbVbcnProcedures#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#26)]  

## <a name="see-also"></a>Consulte também

- [Procedimentos do operador](./operator-procedures.md)
- [Como definir um operador de conversão](./how-to-define-a-conversion-operator.md)
- [Como chamar um procedimento de operador](./how-to-call-an-operator-procedure.md)
- [Como usar uma classe que define operadores](./how-to-use-a-class-that-defines-operators.md)
- [Instrução Operator](../../../language-reference/statements/operator-statement.md)
- [Instrução Structure](../../../language-reference/statements/structure-statement.md)
- [Como: Declarar uma estrutura](../data-types/how-to-declare-a-structure.md)
- [Operador Mod](../../../language-reference/operators/mod-operator.md)
