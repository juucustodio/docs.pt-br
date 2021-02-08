---
description: 'Saiba mais sobre as diretivas: #Disable e #Enable (Visual Basic)'
title: Habilitar e desabilitar diretivas
ms.date: 01/28/2021
helpviewer_keywords:
- directives, enable
- directives, disable
- disable directive
ms.openlocfilehash: d600cc959639a3f70bca5678fbc81aae0806c9cc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797257"
---
# <a name="disable-and-enable-directives-visual-basic"></a>Diretivas #Disable e #Enable (Visual Basic)

As `#Disable` `#Enable` diretivas e são Visual Basic diretivas do compilador de código-fonte. Eles são usados para desabilitar e reabilitar avisos específicos para regiões de código.

```vb
' Suppress warning about no awaits in this method.
#Disable Warning BC42356
    Async Function TestAsync() As Task
        Console.WriteLine("testing")
    End Function
#Enable Warning BC42356
```

Você também pode desabilitar e habilitar uma lista separada por vírgulas de códigos de aviso.

## <a name="see-also"></a>Consulte também

- [Referência de linguagem de Visual Basic](../index.md)
- [Como suprimir avisos de análise de código](../../../fundamentals/code-analysis/suppress-warnings.md)
