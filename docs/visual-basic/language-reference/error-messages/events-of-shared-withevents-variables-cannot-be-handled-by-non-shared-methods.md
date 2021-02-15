---
description: 'Saiba mais sobre: BC30594: eventos de variáveis WithEvents compartilhadas não podem ser tratados por métodos não compartilhados'
title: Eventos de variáveis WithEvents compartilhadas não podem ser identificados por métodos não compartilhados
ms.date: 07/20/2015
f1_keywords:
- bc30594
- vbc30594
helpviewer_keywords:
- BC30594
ms.assetid: 5b9fceb4-ab11-41bb-ad3b-6f1a9da8ae7e
ms.openlocfilehash: f9e8bf6e0d365c4ee747deb6be0e809904d87117
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796412"
---
# <a name="bc30594-events-of-shared-withevents-variables-cannot-be-handled-by-non-shared-methods"></a>BC30594: eventos de variáveis WithEvents compartilhadas não podem ser tratados por métodos não compartilhados

Uma variável declarada com o `Shared` modificador é uma variável compartilhada. Uma variável compartilhada identifica exatamente um local de armazenamento. Uma variável declarada com o `WithEvents` modificador afirma que o tipo ao qual a variável pertence trata o conjunto de eventos que a variável gera. Quando um valor é atribuído à variável, a propriedade criada pela `WithEvents` declaração desvincula qualquer manipulador de eventos existente e conecta o novo manipulador de eventos por meio do `Add` método.

 **ID do erro:** BC30594

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Declare seu manipulador de eventos `Shared` .

## <a name="see-also"></a>Consulte também

- [Compartilhado](../modifiers/shared.md)
- [WithEvents](../modifiers/withevents.md)
