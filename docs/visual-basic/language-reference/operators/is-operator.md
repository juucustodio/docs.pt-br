---
description: 'Saiba mais sobre: operador is (Visual Basic)'
title: É operador
ms.date: 07/20/2015
f1_keywords:
- vb.is
helpviewer_keywords:
- comparison operators [Visual Basic]
- equivalent objects
- TypeOf...Is expression
- Is operator [Visual Basic]
ms.assetid: 8045a6c8-2a83-45b6-ad47-d09a704c656d
ms.openlocfilehash: 0912ebd9bc9c33149568c6cea0197ef24c305ff2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99665676"
---
# <a name="is-operator-visual-basic"></a>Operador is (Visual Basic)

Compara duas variáveis de referência de objeto.

## <a name="syntax"></a>Syntax

```vb
result = object1 Is object2
```

## <a name="parts"></a>Partes

 `result`  
 Obrigatório. Qualquer `Boolean` valor.  
  
 `object1`  
 Obrigatório. Qualquer `Object` nome.  
  
 `object2`  
 Obrigatório. Qualquer `Object` nome.  
  
## <a name="remarks"></a>Comentários

O `Is` operador determina se duas referências de objeto se referem ao mesmo objeto. No entanto, ele não executa comparações de valor. Se `object1` e `object2` ambos se referirem exatamente à mesma instância de objeto, `result` será `True` ; se não forem, `result` será `False` .

> [!NOTE]
> A `Is` palavra-chave também é usada no [Select... Instrução Case](../statements/select-case-statement.md).
  
## <a name="example"></a>Exemplo

O exemplo a seguir usa o `Is` operador para comparar pares de referências de objeto. Os resultados são atribuídos a um `Boolean` valor que representa se os dois objetos são idênticos.

[!code-vb[VbVbalrOperators#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#27)]

Como demonstra o exemplo anterior, você pode usar o `Is` operador para testar os objetos ligados antecipadamente e associação tardia.

## <a name="use-typeof-operator-with-is-operator"></a>Use o operador TypeOf com operador is

`Is` o operador também pode ser usado com a `TypeOf` palavra-chave para criar uma `TypeOf` expressão... `Is` , que testa se uma variável de objeto é compatível com um tipo de dados. Por exemplo:

```vb
If TypeOf sender Is Button Then
```

## <a name="see-also"></a>Confira também

- [Operador TypeOf](typeof-operator.md)
- [Operador IsNot](isnot-operator.md)
- [Operadores de comparação no Visual Basic](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Precedência do operador no Visual Basic](operator-precedence.md)
- [Operadores Listados por Funcionalidade](operators-listed-by-functionality.md)
- [Operadores e expressões](../../programming-guide/language-features/operators-and-expressions/index.md)
