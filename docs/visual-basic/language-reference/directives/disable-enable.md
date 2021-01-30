---
title: Habilitar e desabilitar diretivas
ms.date: 01/28/2021
helpviewer_keywords:
- directives, enable
- directives, disable
- disable directive
ms.openlocfilehash: 3104b25c903465f3a650304f477b25a74591c8ba
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99217222"
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

## <a name="see-also"></a>Confira também

- [Referência de linguagem de Visual Basic](../index.md)
- [Como suprimir avisos de análise de código](../../../fundamentals/code-analysis/suppress-warnings.md)
