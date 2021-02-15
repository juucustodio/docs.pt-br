---
description: 'Saiba mais sobre: instrução Stop (Visual Basic)'
title: Instrução Stop
ms.date: 07/20/2015
f1_keywords:
- vb.Stop
helpviewer_keywords:
- breakpoints, Stop statements
- Stop statements [Visual Basic], syntax
- Stop statements [Visual Basic]
- execution [Visual Basic], suspending
- processing, interrupting
- processes, interrupting
- execution [Visual Basic], stopping
ms.assetid: c9a9fde0-d649-4662-9bef-bd0146ebc2a7
ms.openlocfilehash: 1e25eb88d1b85f38a53023dfb7dfbc877f498e5e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741075"
---
# <a name="stop-statement-visual-basic"></a>Instrução Stop (Visual Basic)

Suspende a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Stop  
```  
  
## <a name="remarks"></a>Comentários  

 Você pode colocar `Stop` instruções em qualquer lugar em procedimentos para suspender a execução. O uso da `Stop` instrução é semelhante à definição de um ponto de interrupção no código.  
  
 A `Stop` instrução suspende a execução, mas, ao contrário `End` , não fecha nenhum arquivo ou limpa nenhuma variável, a menos que seja encontrado em um arquivo executável compilado (. exe).  
  
> [!NOTE]
> Se a `Stop` instrução for encontrada no código que está sendo executado fora do IDE (ambiente de desenvolvimento integrado), o depurador será invocado. Isso é verdadeiro independentemente de o código ter sido compilado no modo de depuração ou de varejo.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa a `Stop` instrução para suspender a execução para cada iteração por meio do `For...Next` loop.  
  
 [!code-vb[VbVbalrStatements#56](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#56)]  
  
## <a name="see-also"></a>Consulte também

- [Instrução End](end-statement.md)
