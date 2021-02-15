---
description: 'Saiba mais sobre a instrução: REM (Visual Basic)'
title: Instrução REM
ms.date: 07/20/2015
f1_keywords:
- vb.'
- vb.Rem
- Rem
- "'"
helpviewer_keywords:
- REM statement [Visual Basic]
- comments, Visual Basic code
- code comments, Visual Basic
- Visual Basic code, comments
- "' comment marker character [Visual Basic]"
ms.assetid: 34126d7f-e0f9-476d-91e6-b31b398615dc
ms.openlocfilehash: c82621db98dc66060ae098ee6537ee58b24046a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741309"
---
# <a name="rem-statement-visual-basic"></a>Instrução REM (Visual Basic)

Usado para incluir comentários explicativos no código-fonte de um programa.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
REM comment  
' comment  
```  
  
## <a name="parts"></a>Partes  

 `comment`  
 Opcional. O texto de qualquer comentário que você deseja incluir. Um espaço é necessário entre a `REM` palavra-chave e `comment` .  
  
## <a name="remarks"></a>Comentários  

 Você pode colocar uma `REM` instrução sozinha em uma linha ou pode colocá-la em uma linha após outra instrução. A `REM` instrução deve ser a última instrução na linha. Se ele seguir outra instrução, o `REM` deverá ser separado dessa instrução por um espaço.  
  
 Você pode usar uma aspa simples ( `'` ) em vez de `REM` . Isso é verdadeiro se o comentário segue outra instrução na mesma linha ou fica sozinho em uma linha.  
  
> [!NOTE]
> Você não pode continuar uma `REM` instrução usando uma sequência de continuação de linha ( `_` ). Depois que um comentário é iniciado, o compilador não examina os caracteres para obter um significado especial. Para um comentário de várias linhas, use outra `REM` instrução ou um símbolo de comentário ( `'` ) em cada linha.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir ilustra a `REM` instrução, que é usada para incluir comentários explicativos em um programa. Ele também mostra a alternativa de usar o caractere de aspa simples ( `'` ) em vez de `REM` .  
  
 [!code-vb[VbVbalrStatements#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>Consulte também

- [Comentários no código](../../programming-guide/program-structure/comments-in-code.md)
- [Como: Quebrar e combinar instruções no código](../../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
