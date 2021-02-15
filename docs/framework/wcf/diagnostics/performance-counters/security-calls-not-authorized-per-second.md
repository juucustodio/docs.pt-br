---
description: 'Saiba mais sobre: chamadas de segurança não autorizadas por segundo'
title: Chamadas de Segurança Não Autorizadas por Segundo
ms.date: 03/30/2017
ms.assetid: 0f189767-8c05-478a-8f0b-9228e5d351e5
ms.openlocfilehash: 60e1baf2b1ed1f3dc502608e6667266608010f0c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716205"
---
# <a name="security-calls-not-authorized-per-second"></a>Chamadas de Segurança Não Autorizadas por Segundo

Nome do contador: chamadas de segurança não autorizadas por segundo.  
  
## <a name="description"></a>Descrição  

 Número de chamadas que falharam na autorização nesta operação em um segundo.  
  
 Esse contador é incrementado quando o <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccess%2A> método retorna `false` . Isso indica que a mensagem de entrada é de um usuário válido e protegida corretamente, mas o usuário não está autorizado a realizar tarefas específicas.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a fórmula a seguir.  
  
 (N 1-N 0)/((D 1-D 0)/F)
