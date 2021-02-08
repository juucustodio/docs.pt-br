---
description: 'Saiba mais sobre: Convenção de chamada de DLL incorreta'
title: Convenção de chamada de DLL inválida
ms.date: 07/20/2015
f1_keywords:
- vbrID49
ms.assetid: 7c7def45-b0ab-450f-ad3f-4383dfd9aed7
ms.openlocfilehash: 7e98ce5131d440a12bff4a4630da087102bdc4da
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797088"
---
# <a name="bad-dll-calling-convention"></a>Convenção de chamada de DLL inválida

Os argumentos passados para uma DLL (biblioteca de vínculo dinâmico) devem corresponder exatamente aos esperados pela rotina. As convenções de chamada lidam com número, tipo e ordem de argumentos. Seu programa pode estar chamando uma rotina em uma DLL que está recebendo o tipo errado ou o número de argumentos.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Verifique se todos os tipos de argumento concordam com aqueles especificados na declaração da rotina que você está chamando.  
  
2. Certifique-se de que você está passando o mesmo número de argumentos indicado na declaração da rotina que você está chamando.  
  
3. Se a rotina DLL espera argumentos por valor, certifique-se `ByVal` de que é especificado para esses argumentos na declaração para a rotina.  
  
## <a name="see-also"></a>Consulte também

- [Tipos de erro](../../programming-guide/language-features/error-types.md)
- [Instrução Call](../statements/call-statement.md)
- [Instrução Declare](../statements/declare-statement.md)
