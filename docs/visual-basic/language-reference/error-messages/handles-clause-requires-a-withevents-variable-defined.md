---
description: 'Saiba mais sobre: BC30506: a cláusula Handles requer uma variável WithEvents definida no tipo recipiente ou um de seus tipos base'
title: A cláusula de identificadores requer uma variável WithEvents definida no tipo recipiente ou em um de seus tipos base
ms.date: 07/20/2015
f1_keywords:
- vbc30506
- bc30506
helpviewer_keywords:
- BC30506
ms.assetid: 5b66f6a8-f050-4e03-a57f-a64e85f80cb5
ms.openlocfilehash: 7253a4766b2015ccbe0ae62f64bc10aaca073dc3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796113"
---
# <a name="bc30506-handles-clause-requires-a-withevents-variable-defined-in-the-containing-type-or-one-of-its-base-types"></a>BC30506: a cláusula Handles requer uma variável WithEvents definida no tipo recipiente ou um de seus tipos base

Você não forneceu uma `WithEvents` variável em sua `Handles` cláusula. A `Handles` palavra-chave no final de uma declaração de procedimento faz com que ele manipule eventos gerados por uma variável de objeto declarada usando a `WithEvents` palavra-chave.

**ID do erro:** BC30506

## <a name="to-correct-this-error"></a>Para corrigir este erro

Forneça a `WithEvents` variável necessária.

## <a name="example"></a>Exemplo

No exemplo a seguir, Visual Basic gera um erro de compilador `BC30506` porque a palavra-chave [WithEvents](../modifiers/withevents.md) não é usada na definição da <xref:System.Timers.Timer?displayProperty=nameWithType> instância.

```vb
Imports System.Timers

Module Module1
    Private _timer1 As New Timer() With {.Interval = 1000, .Enabled = True}

    Sub Main()
        Console.WriteLine("Press any key to start the timer...")
        Console.ReadKey()
        _timer1.Start()
        Console.ReadKey()
    End Sub

    Private Sub Timer1_Tick(sender As Object, args As EventArgs) Handles _timer1.Elapsed
        Console.WriteLine("Press any key to terminate...")
    End Sub
End Module
```

O exemplo a seguir é compilado com êxito porque a `_timer1` variável é definida com a `WithEvents` palavra-chave:

```vb
Imports System.Timers

Module Module1
    Private WithEvents _timer1 As New Timer() With {.Interval = 1000}

    Sub Main()
        Console.WriteLine("Press any key to start the timer...")
        Console.ReadKey()
        _timer1.Start()
        Console.ReadKey()
    End Sub

    Private Sub Timer1_Tick(sender As Object, args As EventArgs) Handles _timer1.Elapsed
        Console.WriteLine("Press any key to terminate...")
    End Sub

End Module
```

## <a name="see-also"></a>Consulte também

- [Alças](../statements/handles-clause.md)
