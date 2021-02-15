---
description: 'Saiba mais sobre: <commonBehaviors>'
title: <commonBehaviors>
ms.date: 03/30/2017
ms.assetid: 5260aeca-388d-4e82-94c0-124fa8054cf5
ms.openlocfilehash: 2fa7397a2833623728bcca286682178d1cf3e1df
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802314"
---
# \<commonBehaviors>

A `commonBehaviors` seção só pode ser definida no arquivo de machine.config. Ele define duas coleções filho chamadas `endpointBehaviors` e `serviceBehaviors` .  Cada coleção define elementos de comportamento consumidos por todos os pontos de extremidade do WCF e serviços no computador, respectivamente. Os comportamentos definidos em `endpointBehaviors` são aplicados somente aos clientes, e os comportamentos definidos no `serviceBehaviors` são aplicados somente aos serviços. Se um comportamento for definido em ambas `commonBehaviors` as `behaviors` seções e, o comportamento na `behaviors` seção terá preferência.
