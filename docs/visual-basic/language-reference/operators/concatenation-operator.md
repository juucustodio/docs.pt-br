---
description: 'Saiba mais sobre: &amp; operador (Visual Basic)'
title: Operador &amp;
ms.date: 07/20/2015
f1_keywords:
- vb.&
helpviewer_keywords:
- And (&) operator
- ampersand operator (&)
- '& operator'
- concatenation operators [Visual Basic], syntax
- strings [Visual Basic], concatenating
ms.assetid: fefc3d00-cbf1-475c-8c5e-6fb213b3f85a
ms.openlocfilehash: ba7c94805e805c841d05241fef557ca972a19ae9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99774090"
---
# <a name="amp-operator-visual-basic"></a>&amp; Operador (Visual Basic)

Gera uma concatenação de cadeia de caracteres de duas expressões.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
result = expression1 & expression2  
```  
  
## <a name="parts"></a>Partes  

 `result`  
 Obrigatório. Qualquer `String` `Object` variável ou.  
  
 `expression1`  
 Obrigatório. Qualquer expressão com um tipo de dados que amplia para `String` .  
  
 `expression2`  
 Obrigatório. Qualquer expressão com um tipo de dados que amplia para `String` .  
  
## <a name="remarks"></a>Comentários  

 Se o tipo de dados de `expression1` ou `expression2` não for, mas se `String` expandir para `String` , ele será convertido em `String` . Se um dos tipos de dados não for ampliado para `String` , o compilador gerará um erro.  
  
 O tipo de dados de `result` é `String` . Se uma ou ambas as expressões forem avaliadas como [Nothing](../nothing.md) ou se tiverem um valor de <xref:System.DBNull.Value?displayProperty=nameWithType> , elas serão tratadas como uma cadeia de caracteres com um valor de "".  
  
> [!NOTE]
> O `&` operador pode ser *sobrecarregado*, o que significa que uma classe ou estrutura pode redefinir seu comportamento quando um operando tem o tipo dessa classe ou estrutura. Se o seu código usar esse operador em uma classe ou estrutura desse tipo, certifique-se de entender seu comportamento redefinido. Para obter mais informações, consulte [procedimentos de operador](../../programming-guide/language-features/procedures/operator-procedures.md).  
  
> [!NOTE]
> O caractere de e comercial (&) também pode ser usado para identificar variáveis como tipo `Long` . Para obter mais informações, consulte [tipos de caracteres](../../programming-guide/language-features/data-types/type-characters.md).  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa o `&` operador para forçar a concatenação de cadeia de caracteres. O resultado é um valor de cadeia de caracteres que representa a concatenação dos dois operandos de cadeia de caracteres.  
  
 [!code-vb[VbVbalrOperators#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- [ Operador&=](and-assignment-operator.md)
- [Operadores de concatenação](concatenation-operators.md)
- [Precedência do operador no Visual Basic](operator-precedence.md)
- [Operadores Listados por Funcionalidade](operators-listed-by-functionality.md)
- [Operadores de concatenação no Visual Basic](../../programming-guide/language-features/operators-and-expressions/concatenation-operators.md)
