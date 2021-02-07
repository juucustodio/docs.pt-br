---
description: 'Saiba mais sobre: alargamento (Visual Basic)'
title: Widening
ms.date: 07/20/2015
f1_keywords:
- vb.widening
helpviewer_keywords:
- conversions [Visual Basic], type
- type conversion [Visual Basic]
- conversions [Visual Basic], data type
- Widening keyword [Visual Basic]
- data type conversion [Visual Basic]
ms.assetid: 646ae263-94d3-40a2-b0cc-64f619292f56
ms.openlocfilehash: de290296ba2b7716ba992c6bed46443053048282
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99700696"
---
# <a name="widening-visual-basic"></a>Widening (Visual Basic)

Indica que um operador de conversão ( `CType` ) converte uma classe ou estrutura em um tipo que pode conter todos os valores possíveis da classe ou estrutura original.  
  
## <a name="converting-with-the-widening-keyword"></a>Convertendo com a palavra-chave Widening  

 O procedimento de conversão deve especificar, `Public Shared` além de `Widening` .  
  
 Conversões de alargamento sempre são bem sucedidos em tempo de execução e nunca incorrem em perda de dados. Os exemplos são `Single` to, `Double` `Char` to `String` e um tipo derivado para seu tipo base. Essa última conversão está se ampliando porque o tipo derivado contém todos os membros do tipo base e, portanto, é uma instância do tipo base.  
  
 O código de consumo não precisa usar o `CType` para conversões de ampliação, mesmo se `Option Strict` for `On` .  
  
 A `Widening` palavra-chave pode ser usada neste contexto:  
  
 [Instrução Operator](../statements/operator-statement.md)  
  
 Para obter exemplos de definições de ampliação e limitação de operadores de conversão, consulte [como definir um operador de conversão](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
## <a name="see-also"></a>Consulte também

- [Instrução Operator](../statements/operator-statement.md)
- [Narrowing](narrowing.md)
- [Conversões de Widening e Narrowing](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [Como definir um operador](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [Função CType](../functions/ctype-function.md)
- [Instrução Option Strict](../statements/option-strict-statement.md)
- [Como definir um operador de conversão](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
