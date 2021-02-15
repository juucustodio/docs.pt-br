---
description: "Saiba mais sobre: BC30481: a instrução ' class ' deve terminar com uma ' End Class ' correspondente"
title: Instrução 'Class' deve finalizar com 'End Class' correspondente
ms.date: 07/20/2015
f1_keywords:
- vbc30481
- bc30481
helpviewer_keywords:
- BC30481
ms.assetid: 583f3029-bc3a-4e06-866f-92dbecc46f19
ms.openlocfilehash: b0d2d89e9e3549b24f9c923e271b15b3b02026b3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796771"
---
# <a name="bc30481-class-statement-must-end-with-a-matching-end-class"></a>BC30481: a instrução ' class ' deve terminar com uma ' End Class ' correspondente

`Class` é usado para iniciar um `Class` bloco; portanto, ele só pode aparecer no início do bloco, com uma instrução correspondente que `End Class` termina o bloco. Você tem uma instrução redundante `Class` ou não terminou seu `Class` bloco com `End Class` .

 **ID do erro:** BC30481

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Localize e remova a instrução desnecessária `Class` .

- Conclua o `Class` bloco com uma correspondência `End Class` .

## <a name="see-also"></a>Consulte também

- [\<keyword>Instrução End](../statements/end-keyword-statement.md)
- [Instrução Class](../statements/class-statement.md)
