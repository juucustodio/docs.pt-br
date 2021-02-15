---
description: 'Saiba mais sobre: BC30029: classes derivadas não podem gerar eventos de classe base'
title: As classes derivadas não podem acionar eventos de classe base
ms.date: 07/20/2015
f1_keywords:
- vbc30029
- bc30029
helpviewer_keywords:
- BC30029
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
ms.openlocfilehash: 68546f2654f7c34fcb309d5af68e237d5f1eac79
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796594"
---
# <a name="bc30029-derived-classes-cannot-raise-base-class-events"></a>BC30029: classes derivadas não podem gerar eventos de classe base

Um evento só pode ser gerado a partir do espaço de declaração no qual ele é declarado. Portanto, uma classe não pode gerar eventos de nenhuma outra classe, mesmo uma da qual ele é derivado.

 **ID do erro:** BC30029

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Mova a `Event` instrução ou a `RaiseEvent` instrução para que elas estejam na mesma classe.

## <a name="see-also"></a>Consulte também

- [Instrução Event](../statements/event-statement.md)
- [Instrução RaiseEvent](../statements/raiseevent-statement.md)
