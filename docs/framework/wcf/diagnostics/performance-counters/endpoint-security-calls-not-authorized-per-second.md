---
description: 'Saiba mais sobre: ponto de extremidade: chamadas de segurança não autorizadas por segundo'
title: 'Ponto de extremidade: chamadas de segurança não autorizadas por segundo'
ms.date: 03/30/2017
ms.assetid: c8a1547b-986b-45c1-b302-dea0cd4b516d
ms.openlocfilehash: 55a49091426538304aceda52308e3f8df2010d6d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99655455"
---
# <a name="endpoint-security-calls-not-authorized-per-second"></a>Ponto de extremidade: chamadas de segurança não autorizadas por segundo

Nome do contador: chamadas de segurança não autorizadas por segundo.  
  
## <a name="description"></a>Descrição  

 Número de mensagens de entrada em um segundo que são de um usuário válido e protegidas corretamente, mas o usuário não está autorizado a realizar tarefas específicas.  
  
 Esse contador é incrementado quando o <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccess%2A> método retorna `false` .  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
