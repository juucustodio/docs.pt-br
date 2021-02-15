---
description: "Saiba mais sobre: BC30014: ' #ElseIf ' deve ser precedido por ' #If ' ou ' #ElseIf ' correspondente"
title: "'#ElseIf' deve ser precedido por um '#If' ou '#ElseIf' correspondente"
ms.date: 07/20/2015
f1_keywords:
- vbc30014
- bc30014
helpviewer_keywords:
- BC30014
ms.assetid: 5215585e-2efa-485a-9efe-9833a1cc83a0
ms.openlocfilehash: 5eeb9c2fc0fd7267d95a8713a7071cd08788e48b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796555"
---
# <a name="bc30014-elseif-must-be-preceded-by-a-matching-if-or-elseif"></a>BC30014: ' #ElseIf ' deve ser precedido por ' #If ' ou ' #ElseIf ' correspondente

`#ElseIf` é uma diretiva de compilação condicional. Uma `#ElseIf` cláusula deve ser precedida por uma `#If` cláusula or correspondente `#ElseIf` .

 **ID do erro:** BC30014

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Verifique se um `#If` ou anterior `#ElseIf` não foi separado dele `#ElseIf` por um bloco de compilação condicional intermediário ou foi colocado incorretamente `#End If` .

2. Se o `#ElseIf` for precedido por uma `#Else` diretiva, remova `#Else` ou altere-o para um `#ElseIf` .

3. Se todo o resto estiver em ordem, adicione uma `#If` diretiva ao início do bloco de compilação condicional.

## <a name="see-also"></a>Consulte também

- [#If... Diretivas then... #Else](../directives/if-then-else-directives.md)
