---
description: 'Saiba mais sobre: operador AddressOf (Visual Basic)'
title: Operador AddressOf
ms.date: 07/20/2015
f1_keywords:
- AddressOf
- vb.AddressOf
helpviewer_keywords:
- AddressOf operator [Visual Basic]
- addresses, passing to API procedures
ms.assetid: 8105a59d-60d8-4ab5-b221-5899cdfacbf4
ms.openlocfilehash: 2aba8c26aa9581fe1070574b8c408e09bf063d1f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99774376"
---
# <a name="addressof-operator-visual-basic"></a>Operador AddressOf (Visual Basic)

Cria uma instância delegada que faz referência ao procedimento específico.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
AddressOf procedurename  
```  
  
## <a name="parts"></a>Partes  

 `procedurename`  
 Obrigatório. Especifica o procedimento a ser referenciado pelo delegado recém-criado.  
  
## <a name="remarks"></a>Comentários  

 O `AddressOf` operador cria um delegado que aponta para a sub-rotina ou função especificada por `procedurename` . Quando o procedimento especificado é um método de instância, o delegado se refere à instância e ao método. Em seguida, quando o delegado é invocado, o método especificado da instância especificada é chamado.  
  
 O `AddressOf` operador pode ser usado como o operando de um construtor delegado ou pode ser usado em um contexto no qual o tipo do delegado possa ser determinado pelo compilador.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa o `AddressOf` operador para designar um delegado para manipular o `Click` evento de um botão.  
  
 [!code-vb[VbVbalrDelegates#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#8)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa o `AddressOf` operador para designar a função de inicialização para um thread.  
  
 [!code-vb[VbVbalrDelegates#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>Consulte também

- [Instrução Declare](../statements/declare-statement.md)
- [Instrução Function](../statements/function-statement.md)
- [Instrução Sub](../statements/sub-statement.md)
- [Representantes](../../programming-guide/language-features/delegates/index.md)
