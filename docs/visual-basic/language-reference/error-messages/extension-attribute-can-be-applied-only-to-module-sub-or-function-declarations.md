---
description: "Saiba mais sobre: BC36550: o atributo ' extension ' só pode ser aplicado a declarações ' module ', ' Sub ' ou ' function '"
title: O atributo 'Extension' pode ser aplicado apenas às declarações 'Module', 'Sub' ou 'Function'
ms.date: 07/20/2015
f1_keywords:
- bc36550
- vbc36550
helpviewer_keywords:
- BC36550
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
ms.openlocfilehash: f0c87de34238974229bc572a0f634a16e8cc78d9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796308"
---
# <a name="bc36550-extension-attribute-can-be-applied-only-to-module-sub-or-function-declarations"></a>BC36550: o atributo ' extension ' só pode ser aplicado a declarações ' module ', ' Sub ' ou ' function '

A única maneira de estender um tipo de dados no Visual Basic é definir um método de extensão dentro de um módulo padrão. O método de extensão pode ser um `Sub` procedimento ou um `Function` procedimento. Todos os métodos de extensão devem ser marcados com o atributo de extensão, `<Extension()>` , do <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> namespace. Opcionalmente, um módulo que contém um método de extensão pode ser marcado da mesma maneira. Nenhum outro uso do atributo de extensão é válido.

**ID do erro:** BC36550

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Remova o atributo de extensão.

- Reprojete sua extensão como um método, definido em um módulo delimitador.

## <a name="example"></a>Exemplo

O exemplo a seguir define um `Print` método para o `String` tipo de dados.

```vb
Imports StringUtility
Imports System.Runtime.CompilerServices
Namespace StringUtility
    <Extension()>
    Module StringExtensions
        <Extension()>
        Public Sub Print (ByVal str As String)
            Console.WriteLine(str)
        End Sub
    End Module
End Namespace
```

## <a name="see-also"></a>Consulte também

- [Visão geral de atributos](../../programming-guide/concepts/attributes/index.md)
- [Métodos de Extensão](../../programming-guide/language-features/procedures/extension-methods.md)
- [Instrução Module](../statements/module-statement.md)
