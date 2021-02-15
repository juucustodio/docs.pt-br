---
description: "Saiba mais sobre: BC32022: ' <eventname> ' é um evento e não pode ser chamado diretamente"
title: "'<eventname>' é um evento, e não pode ser chamado diretamente"
ms.date: 07/20/2015
f1_keywords:
- bc32022
- vbc32022
helpviewer_keywords:
- BC32022
ms.assetid: 4dcfcb8d-a9fa-46a7-a034-29d9ff3a59b3
ms.openlocfilehash: f9d4b8fe54e1101e7963933f871cf5af2c1af903
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796438"
---
# <a name="bc32022-eventname-is-an-event-and-cannot-be-called-directly"></a>BC32022: ' \<eventname> ' é um evento e não pode ser chamado diretamente

' <`eventname`> ' é um evento e, portanto, não pode ser chamado diretamente. Use uma `RaiseEvent` instrução para gerar um evento.

 Uma chamada de procedimento especifica um evento para o nome do procedimento. Um manipulador de eventos é um procedimento, mas o evento em si é um dispositivo de sinalização, que deve ser gerado e manipulado.

 **ID do erro:** BC32022

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Use uma `RaiseEvent` instrução para sinalizar um evento e invocar o procedimento ou procedimentos que o manipulam.

## <a name="see-also"></a>Consulte também

- [Instrução RaiseEvent](../statements/raiseevent-statement.md)
