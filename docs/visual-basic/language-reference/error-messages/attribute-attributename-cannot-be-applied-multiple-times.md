---
description: "Saiba mais sobre: BC30663: o atributo ' <attributename> ' não pode ser aplicado várias vezes"
title: O atributo '<attributename>' não pode ser aplicado várias vezes
ms.date: 07/20/2015
f1_keywords:
- bc30663
- vbc30663
helpviewer_keywords:
- BC30663
ms.assetid: 3760e7ff-7238-40a1-8676-77d858a64fc0
ms.openlocfilehash: 84b77111a7401eb6f30eb7cd167f4b5689f33e77
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797140"
---
# <a name="bc30663-attribute-attributename-cannot-be-applied-multiple-times"></a>BC30663: o atributo ' \<attributename> ' não pode ser aplicado várias vezes

O atributo só pode ser aplicado uma vez. O `AttributeUsage` atributo determina se um atributo pode ser aplicado mais de uma vez.

 **ID do erro:** BC30663

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Verifique se o atributo é aplicado apenas uma vez.

2. Se você estiver usando atributos personalizados que desenvolveu, considere alterar seu `AttributeUsage` atributo para permitir o uso de vários atributos, como no exemplo a seguir.

```vb
<AttributeUsage(AllowMultiple := True)>
```

## <a name="see-also"></a>Consulte também

- <xref:System.AttributeUsageAttribute>
- [Criando atributos personalizados](../../programming-guide/concepts/attributes/creating-custom-attributes.md)
- [AttributeUsage](../../programming-guide/concepts/attributes/attributeusage.md)
