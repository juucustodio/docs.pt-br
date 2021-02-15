---
description: 'Saiba mais sobre: ByVal (Visual Basic)'
title: ByVal
ms.date: 07/20/2015
f1_keywords:
- vb.ByVal
- ByVal
helpviewer_keywords:
- ByVal keyword [Visual Basic], contexts
- ByVal keyword [Visual Basic]
ms.assetid: 1eaf4e58-b305-4785-9e3d-e416b9c75598
ms.openlocfilehash: cd7116c0bcc3d263cc2bb6a9b95e46e8ff0cc116
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99774610"
---
# <a name="byval-visual-basic"></a>ByVal (Visual Basic)

Especifica que um argumento é passado [por valor](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md), de modo que o procedimento chamado ou a propriedade não possa alterar o valor de uma variável subjacente ao argumento no código de chamada. Se nenhum modificador for especificado, ByVal será o padrão.

> [!NOTE]
> Como é o padrão, você não precisa especificar explicitamente a `ByVal` palavra-chave em assinaturas de método. Ele tende a produzir código barulhento e, muitas vezes, leva à `ByRef` palavra-chave não-padrão que está sendo ignorada.

## <a name="remarks"></a>Comentários

 O `ByVal` modificador pode ser usado nesses contextos:

 [Instrução Declare](../statements/declare-statement.md)

 [Instrução Function](../statements/function-statement.md)
  
 [Instrução Operator](../statements/operator-statement.md)
  
 [Instrução Property](../statements/property-statement.md)
  
 [Instrução Sub](../statements/sub-statement.md)

## <a name="example"></a>Exemplo

 O exemplo a seguir demonstra o uso do `ByVal` mecanismo de passagem de parâmetro com um argumento de tipo de referência. No exemplo, o argumento é `c1` uma instância da classe `Class1` . `ByVal` impede que o código nos procedimentos altere o valor subjacente do argumento de referência, `c1` , mas não protege os campos e as propriedades acessíveis do `c1` .

 [!code-vb[VbVbalrKeywords#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class5.vb#10)]

## <a name="see-also"></a>Consulte também

- [Palavras-chave](../keywords/index.md)
- [Passar argumentos por valor e por referência](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
