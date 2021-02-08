---
description: 'Saiba mais sobre: MustOverride (Visual Basic)'
title: MustOverride
ms.date: 07/20/2015
f1_keywords:
- vb.MustOverride
- MustOverride
helpviewer_keywords:
- virtual elements [Visual Basic], pure
- elements [Visual Basic], pure virtual
- properties [Visual Basic], redefining
- procedures [Visual Basic], overriding
- overriding, MustOverride keyword
- procedures [Visual Basic], redefining
- pure virtual elements [Visual Basic]
- MustOverride keyword [Visual Basic]
- properties [Visual Basic], overriding
ms.assetid: 6e9d9ad6-bb64-433f-b32b-3ef84293bf96
ms.openlocfilehash: df7200a7f7ec4bfda34765747d6318bc50a38dd1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99774519"
---
# <a name="mustoverride-visual-basic"></a>MustOverride (Visual Basic)

Especifica que uma propriedade ou procedimento não está implementado nesta classe e deve ser substituído em uma classe derivada antes que possa ser usado.  
  
## <a name="remarks"></a>Comentários  

 Você pode usar `MustOverride` somente em uma instrução de declaração de propriedade ou de procedimento. A propriedade ou procedimento que especifica `MustOverride` deve ser um membro de uma classe e a classe deve ser marcada como [MustInherit](mustinherit.md).  
  
## <a name="rules"></a>Regras  
  
- **Declaração incompleta.** Quando você especifica `MustOverride` , você não fornece nenhuma linha adicional de código para a propriedade ou procedimento, nem mesmo a `End Function` instrução, `End Property` ou `End Sub` .  
  
- **Modificadores combinados.** Você não pode especificar `MustOverride` juntos com `NotOverridable` , `Overridable` ou `Shared` na mesma declaração.  
  
- **Sombreamento e substituição.** Sombreamento e substituição redefinem um elemento herdado, mas há diferenças significativas entre as duas abordagens. Para obter mais informações, consulte [sombreamento em Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md).  
  
- **Termos alternativos.** Um elemento que não pode ser usado, exceto em uma substituição, às vezes é chamado de elemento *virtual puro* .  
  
 O `MustOverride` modificador pode ser usado nesses contextos:  
  
 [Instrução Function](../statements/function-statement.md)  
  
 [Instrução Property](../statements/property-statement.md)  
  
 [Instrução Sub](../statements/sub-statement.md)  
  
## <a name="see-also"></a>Consulte também

- [NotOverridable](notoverridable.md)
- [Substituível](overridable.md)
- [Substituições](overrides.md)
- [MustInherit](mustinherit.md)
- [Palavras-chave](../keywords/index.md)
- [Sombreamento no Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md)
