---
description: 'Saiba mais sobre: propagação de ID de atividade'
title: Propagação de ID de atividade
ms.date: 03/30/2017
ms.assetid: cd1c1ae5-cc8a-4f51-90c9-f7b476bcfe70
ms.openlocfilehash: d407af04304298bcc04a7aa4264eb6fc46563d3a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99770892"
---
# <a name="activity-id-propagation"></a>Propagação de ID de atividade

A propagação ocorre quando o rastreamento de atividade ServiceModel está habilitado (propagação de ServiceModel) ou desabilitado (propagação de atividade de usuário para usuário).  
  
## <a name="servicemodel-activity-tracing-is-enabled"></a>Rastreamento de atividade de ServiceModel está habilitado  

 Se o ServiceModel ActivityTracing estiver habilitado, a propagação ocorrerá entre as atividades processAction.  
  
### <a name="server"></a>Servidor  

 Quando o `propagateActivity` atributo é definido como `true` no cliente e no servidor, a ID da `ProcessAction` atividade no servidor é idêntica à ID no cabeçalho da mensagem propagada `ActivityId` .  
  
 Quando nenhum `ActivityId` cabeçalho estiver presente na mensagem (ou seja, `propagateActivity` = `false` no cliente) ou quando estiver `propagateActivity` = `false` no servidor, o servidor gerará uma nova ID de atividade.  
  
### <a name="client"></a>Cliente  

 Se o cliente tiver um thread único de forma síncrona, o cliente desconsiderará todas as configurações do `propagateActivity` no cliente ou servidor. Em vez disso, a resposta é tratada na atividade de solicitação. Se o cliente for assíncrono ou síncrono com multithread, `propagateActivity` = `true` no cliente e houver um cabeçalho de ID de atividade na mensagem enviada pelo servidor, o cliente recuperará a ID da atividade e transferirá para a atividade processar ação que contém a ID da atividade propagada. Caso contrário, o cliente transfere da atividade processar mensagem para uma nova atividade processar ação. Essa atividade de transferência extra para uma nova ação de processo é feita para consistência. Dentro dessa atividade, o cliente recupera a ID de atividade da atividade BeginCall do contexto de thread local, quando o thread é alocado para o processamento de mensagens de resposta. Em seguida, ele transfere para a atividade de ação de processo inicial.  
  
 Se o cliente for duplex, o cliente atuará como servidor ao receber a mensagem.  
  
### <a name="propagation-in-fault-messages"></a>Propagação em mensagens de falha  

 Não há nenhuma diferença no tratamento de mensagens válidas e de falha. Se `propagateActivity` = `true` , a ID da atividade adicionada aos cabeçalhos de mensagem de falha SOAP é idêntica à atividade ambiente.  
  
## <a name="servicemodel-activity-tracing-is-disabled"></a>Rastreamento de atividade de ServiceModel desabilitado  

 Se o ServiceModel ActivityTracing estiver desabilitado, a propagação ocorrerá entre as atividades de código do usuário diretamente sem passar pelas atividades de ServiceModel. Uma ID de atividade definida pelo usuário também é propagada por meio do cabeçalho de ID de atividade da mensagem.  
  
 Se `propagateActivity` = `true` e `ActivityTracing` = `off` para um ouvinte de rastreamento de ServiceModel (independentemente de o rastreamento estar habilitado no ServiceModel), acontecerá o seguinte no cliente ou no servidor:  
  
- Na solicitação da operação ou no envio de resposta, a ID da atividade em TLS é propagada para fora do código do usuário até que uma mensagem seja formada. Um cabeçalho de ID de atividade também é inserido na mensagem antes de ser enviado.  
  
- Ao receber a solicitação ou receber resposta, a ID da atividade é recuperada do cabeçalho da mensagem assim que o objeto da mensagem recebida é criado. A ID da atividade em TLS é propagada assim que a mensagem desaparece do escopo até que o código do usuário seja atingido.  
  
 Essas ações garantem que os rastreamentos de usuário serão exibidos na mesma atividade se a propagação estiver ativada. No entanto, ele não faz nenhuma garantia em rastreamentos de ServiceModel. Os rastreamentos de ServiceModel ocorrerão em uma atividade de código do usuário somente se o processamento desses rastreamentos for executado no mesmo thread em que a atividade de código do usuário foi definida.  
  
 Em geral, os rastreamentos de ServiceModel podem ser observados nos seguintes locais:  
  
- Se o rastreamento de ServiceModel estiver desabilitado, todos os rastreamentos emitidos aparecerão nas atividades do usuário. Se a propagação estiver habilitada no servidor e no cliente, esses rastreamentos estarão na mesma atividade.  
  
- Se o rastreamento de ServiceModel estiver habilitado, mas ActivityTracing estiver desabilitado, os rastreamentos de usuário aparecerão na mesma atividade se a propagação estiver habilitada em ambas as extremidades. Os rastreamentos de ServiceModel aparecem na atividade 0000 padrão, a menos que ocorram no mesmo thread que o processamento de código de usuário em que a atividade está inicialmente definida.  
  
- Se o rastreamento de ServiceModel e ActivityTracing estiverem habilitados, os rastreamentos de usuário aparecerão em atividades definidas pelo usuário e os rastreamentos de ServiceModel aparecerão em atividades definidas pelo ServiceModel. A propagação ocorre no nível de ServiceModel.
