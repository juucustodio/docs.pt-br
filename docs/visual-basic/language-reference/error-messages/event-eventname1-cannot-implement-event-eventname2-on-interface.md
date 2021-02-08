---
description: "Saiba mais sobre: BC31423: o evento ' <eventname1> ' não pode implementar o evento ' <eventname2> ' na interface ' <interface> ' porque seus tipos delegados ' <delegate1> ' e ' <delegate2> ' não correspondem"
title: O evento '<eventname1>' não pode implementar o evento '<eventname2>' na interface '<interface>' porque seus tipos delegados '<delegate1>' e '<delegate2>' não correspondem.
ms.date: 07/20/2015
f1_keywords:
- vbc31423
- bc31423
helpviewer_keywords:
- BC31423
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
ms.openlocfilehash: cfb967d2b43ce1f34f56f3d019a9a663b000296c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796451"
---
# <a name="bc31423-event-eventname1-cannot-implement-event-eventname2-on-interface-interface-because-their-delegate-types-delegate1-and-delegate2-do-not-match"></a>BC31423: o evento ' \<eventname1> ' não pode implementar \<eventname2> o evento ' ' na interface ' \<interface> ' porque seus tipos delegados ' \<delegate1> ' e ' \<delegate2> ' não correspondem

Visual Basic não pode implementar um evento porque o tipo delegado do evento não corresponde ao tipo delegado do evento na interface. Esse erro pode ocorrer quando você define vários eventos em uma interface e, em seguida, tenta implementá-los junto com o mesmo evento. Um evento pode implementar dois ou mais eventos somente se todos os eventos implementados forem declarados usando a `As` sintaxe e especificarem o mesmo tipo de delegado.

 **ID do erro:** BC31423

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Implemente os eventos separadamente.

     — ou —

- Defina os eventos na interface usando a `As` sintaxe e especifique o mesmo tipo de delegado.

## <a name="see-also"></a>Consulte também

- [Instrução Event](../statements/event-statement.md)
- [Instrução Delegate](../statements/delegate-statement.md)
- [Eventos](../../programming-guide/language-features/events/index.md)
