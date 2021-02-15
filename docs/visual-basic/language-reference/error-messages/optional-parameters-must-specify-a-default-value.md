---
description: 'Saiba mais sobre: BC30812: parâmetros opcionais devem especificar um valor padrão'
title: Parâmetros opcionais devem especificar um valor padrão
ms.date: 07/20/2015
f1_keywords:
- vbc30812
- bc30812
helpviewer_keywords:
- BC30812
ms.assetid: 5091a250-be66-413b-98a3-2a9974c4d600
ms.openlocfilehash: 1cbed1c0f1297ecacdae94d9234d18a3d268f487
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795528"
---
# <a name="bc30812-optional-parameters-must-specify-a-default-value"></a>BC30812: parâmetros opcionais devem especificar um valor padrão

Parâmetros opcionais devem fornecer valores padrão que podem ser usados se nenhum parâmetro for fornecido por um procedimento de chamada.

**ID do erro:** BC30812

## <a name="example"></a>Exemplo

O exemplo a seguir gera BC30812:

```vb
Sub Proc1(x As Integer, Optional y As String)
    Console.WriteLine("Default argument is: " & y)
End Sub
```

## <a name="to-correct-this-error"></a>Para corrigir este erro

Especifique valores padrão para parâmetros opcionais:

```vb
Sub Proc1(x As Integer, Optional y As String = "Default Value")
    Console.WriteLine("Default argument is: " & y)
End Sub
```

## <a name="see-also"></a>Consulte também

- [Opcional](../modifiers/optional.md)
