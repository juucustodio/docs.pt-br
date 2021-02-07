---
description: 'Saiba mais sobre: MSMQ'
title: MSMQ
ms.date: 03/30/2017
ms.assetid: d9fca29f-fa44-4ec4-bb48-b10800694500
ms.openlocfilehash: 3d694fdab202cd2b3b03c377f72d93c22cbae263
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720573"
---
# <a name="msmq"></a>MSMQ

Em um aplicativo MSMQ, nenhuma atividade adicional é transferida do canal enfileirado para MSMQ e do MSMQ para o canal em fila.  
  
 Além disso, a ID da mensagem do MSMQ e a ID da mensagem SOAP (juntamente com a ID da atividade, se houver) são rastreadas como parte dos rastreamentos de canal na fila em uma operação de envio.  
  
 A ID da mensagem do MSMQ e a ID da mensagem SOAP (juntamente com a ID da atividade, se houver) são rastreadas como parte dos rastreamentos de canal na fila em uma operação de recebimento.  
  
 As transferências necessárias na operação de recebimento são executadas de forma semelhante a qualquer outro transporte (>de mensagens de processo de recebimento de bytes-> operação).
