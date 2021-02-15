---
title: Operador NameOf
description: Saiba como usar o operador NameOf no Visual Basic
ms.date: 10/27/2019
f1_keywords:
- NameOf
- vb.NameOf
helpviewer_keywords:
- NameOf operator [Visual Basic]
ms.openlocfilehash: 0e72c4cb0c10113e53067ea4a743ca5ee77bcc95
ms.sourcegitcommit: 43ed174f085840ca18a791dc89fe833174da766d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828897"
---
# <a name="nameof-operator---visual-basic"></a>Operador NameOf-Visual Basic

O operador `NameOf` obtém o nome de uma variável, tipo ou membro como uma cadeia de caracteres constante:

```vb
Console.WriteLine(NameOf(System.Collections.Generic))  ' output: Generic
Console.WriteLine(NameOf(List(Of Integer)))  ' output: List
Console.WriteLine(NameOf(List(Of Integer).Count))  ' output: Count
Console.WriteLine(NameOf(List(Of Integer).Add))  ' output: Add

Dim numbers As New List(Of Integer) From { 1, 2, 3 }
Console.WriteLine(NameOf(numbers))  ' output: numbers
Console.WriteLine(NameOf(numbers.Count))  ' output: Count
Console.WriteLine(NameOf(numbers.Add))  ' output: Add
```

Como mostra o exemplo anterior, no caso de um tipo e um namespace, o nome produzido geralmente não é [totalmente qualificado](~/_csharplang/spec/basic-concepts.md#fully-qualified-names).

O operador `NameOf` é avaliado no tempo de compilação e não tem efeitos no tempo de execução.

Você pode usar o operador `NameOf` para tornar o código de verificação de argumentos mais passível de manutenção:

```vb
Private _name As String

Public Property Name As String
    Get
        Return _name
    End Get
    Set
        If value Is Nothing Then
            Throw New ArgumentNullException(NameOf(value), $"{NameOf(name)} cannot be null.")
        End If
    End Set
End Property
```

O `NameOf` operador está disponível no Visual Basic 14 e posterior.

## <a name="see-also"></a>Consulte também

- [Referência da linguagem Visual Basic](../index.md)
- [Operadores (Visual Basic)](index.md)
