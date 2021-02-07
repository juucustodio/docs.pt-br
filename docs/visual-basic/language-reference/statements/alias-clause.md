---
description: 'Saiba mais sobre: cláusula de alias (Visual Basic)'
title: Cláusula Alias
ms.date: 07/20/2015
f1_keywords:
- vb.Alias
helpviewer_keywords:
- Alias keyword [Visual Basic]
ms.assetid: 58c06b11-465d-4d87-906a-73200a3d7f19
ms.openlocfilehash: bf0ee1c22105b29aedb99ce45a99ba866f4b93c1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99674071"
---
# <a name="alias-clause-visual-basic"></a>Cláusula Alias (Visual Basic)

Indica que um procedimento externo tem outro nome em sua DLL.  
  
## <a name="remarks"></a>Comentários  

 A `Alias` palavra-chave pode ser usada neste contexto:  
  
 [Instrução Declare](declare-statement.md)  
  
 No exemplo a seguir, a `Alias` palavra-chave é usada para fornecer o nome da função em advapi32.dll, `GetUserNameA` que `getUserName` é usada no lugar deste exemplo. A função `getUserName` é chamada em sub `getUser` , que exibe o nome do usuário atual.  
  
 [!code-vb[VbVbalrStatements#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>Consulte também

- [Palavras-chave](../keywords/index.md)
