---
description: 'Saiba mais sobre: operador TypeOf (Visual Basic)'
title: Operador TypeOf
ms.date: 07/20/2015
f1_keywords:
- TypeOf
- vb.TypeOf
helpviewer_keywords:
- types [Visual Basic], compatible
- comparison operators [Visual Basic]
- TypeOf...Is expression
- data types [Visual Basic], compatible
- TypeOf operator [Visual Basic]
- compatible data types [Visual Basic]
ms.assetid: 33f65296-659a-4b9a-9a29-c2a91cff68b2
ms.openlocfilehash: 59a03095b2abbaa304221b30402b9a058954db63
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795229"
---
# <a name="typeof-operator-visual-basic"></a>Operador TypeOf (Visual Basic)

Verifica se o tipo de tempo de execução do resultado de uma expressão é compatível com tipo com o tipo especificado.
  
## <a name="syntax"></a>Syntax  
  
```vb  
result = TypeOf objectexpression Is typename  
```  
  
```vb  
result = TypeOf objectexpression IsNot typename  
```  
  
## <a name="parts"></a>Partes  

 `result`  
 Exibido. Um valor `Boolean`.  
  
 `objectexpression`  
 Obrigatório. Qualquer expressão que seja avaliada como um tipo de referência.  
  
 `typename`  
 Obrigatório. Qualquer nome de tipo de dados.  
  
## <a name="remarks"></a>Comentários  

 O `TypeOf` operador determina se o tipo de tempo de execução do `objectexpression` é compatível com `typename` . A compatibilidade depende da categoria de tipo de `typename` . A tabela a seguir mostra como a compatibilidade é determinada.  
  
|Categoria de tipo de `typename`|Critério de compatibilidade|  
|---------------------------------|-----------------------------|  
|Class|`objectexpression` é do tipo `typename` ou herda de `typename`|  
|Estrutura|`objectexpression` é do tipo `typename`|  
|Interface|`objectexpression` implementa `typename` ou herda de uma classe que implementa `typename`|  
  
 Se o tipo de tempo de execução `objectexpression` atende ao critério de compatibilidade, `result` é `True` . Caso contrário, `result` é `False`.  Se `objectexpression` for NULL, então `TypeOf` ... `Is` retorna `False` e... `IsNot` retorna `True` .  
  
 `TypeOf` é sempre usado com a `Is` palavra-chave para construir uma `TypeOf` expressão... `Is` ou com a `IsNot` palavra-chave para construir uma `TypeOf` expressão... `IsNot` .  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa `TypeOf` expressões... `Is` para testar a compatibilidade de tipo de duas variáveis de referência de objeto com vários tipos de dados.  
  
 [!code-vb[VbVbalrOperators#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#39)]  
  
 A variável `refInteger` tem um tipo de tempo de execução de `Integer` . Ele é compatível com `Integer` , mas não com `Double` . A variável `refForm` tem um tipo de tempo de execução de <xref:System.Windows.Forms.Form> . Ele é compatível com <xref:System.Windows.Forms.Form> porque é seu tipo, com <xref:System.Windows.Forms.Control> porque <xref:System.Windows.Forms.Form> herda de <xref:System.Windows.Forms.Control> e com <xref:System.ComponentModel.IComponent> porque <xref:System.Windows.Forms.Form> herda de <xref:System.ComponentModel.Component> , que implementa <xref:System.ComponentModel.IComponent> . No entanto, o `refForm` não é compatível com o <xref:System.Windows.Forms.Label> .  
  
## <a name="see-also"></a>Consulte também

- [Operador Is](is-operator.md)
- [Operador IsNot](isnot-operator.md)
- [Operadores de comparação no Visual Basic](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Precedência do operador no Visual Basic](operator-precedence.md)
- [Operadores Listados por Funcionalidade](operators-listed-by-functionality.md)
- [Operadores e expressões](../../programming-guide/language-features/operators-and-expressions/index.md)
