---
description: 'Saiba mais sobre: BC32098: os parâmetros de tipo não podem ser usados como qualificadores'
title: Não é possível usar parâmetros de tipo como qualificadores
ms.date: 07/20/2015
f1_keywords:
- vbc32098
- bc32098
helpviewer_keywords:
- BC32098
ms.assetid: bab05325-dde8-4621-a5f6-368b5b7b2d76
ms.openlocfilehash: 61be8e81c9cf6c7a8339c7bbf0ad9566f582eb57
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675046"
---
# <a name="bc32098-type-parameters-cannot-be-used-as-qualifiers"></a>BC32098: parâmetros de tipo não podem ser usados como qualificadores

Um elemento de programação é qualificado com uma cadeia de caracteres de qualificação que inclui um parâmetro de tipo.

Um parâmetro de tipo representa um requisito para um tipo que deve ser fornecido quando o tipo genérico é construído. Ele não representa um tipo definido específico. Uma cadeia de caracteres de qualificação deve incluir apenas elementos que são definidos no momento da compilação.

O código a seguir pode gerar esse erro:

```vb
Public Function CheckText(Of c As System.Windows.Forms.Control)(
    badText As String) As Boolean

    Dim saveText As c.Text
    ' Insert code to look for badText within saveText.
End Function
```

 **ID do erro:** BC32098

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Remova o parâmetro de tipo da cadeia de caracteres de qualificação ou substitua-o por um tipo definido.

2. Se você precisar usar um tipo construído para localizar o elemento de programação que está sendo qualificado, deverá usar a lógica de programa adicional.

## <a name="see-also"></a>Consulte também

- [Referências a elementos declarados](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Tipos genéricos no Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [Lista de Tipos](../statements/type-list.md)
