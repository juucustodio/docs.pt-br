---
description: 'Saiba mais sobre: ataques de repetição'
title: Ataques por repetição
ms.date: 03/30/2017
ms.assetid: 7a17e040-93cd-4432-81b9-9f62fec78c8f
ms.openlocfilehash: b367bd6238f85471871c59b393a8f28a40c4ddba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99632848"
---
# <a name="replay-attacks"></a>Ataques por repetição

Um *ataque de reprodução* ocorre quando um invasor copia um fluxo de mensagens entre duas partes e repete o fluxo para uma ou mais das partes. A menos que seja atenuado, os computadores sujeitos ao ataque processam o fluxo como mensagens legítimas, resultando em uma variedade de consequências inadequadas, como ordens redundantes de um item.  
  
## <a name="bindings-may-be-subject-to-reflection-attacks"></a>As associações podem estar sujeitas a ataques de reflexo  

 Os *ataques de reflexo* são repetições de mensagens de volta para um remetente como se tivessem vindo do receptor como resposta. A *detecção de reprodução* padrão no mecanismo de Windows Communication Foundation (WCF) não trata isso automaticamente.  
  
 Os ataques de reflexão são mitigados por padrão porque o modelo de serviço do WCF adiciona uma ID de mensagem assinada para solicitar mensagens e espera um `relates-to` cabeçalho assinado em mensagens de resposta. Consequentemente, a mensagem de solicitação não pode ser repetida como uma resposta. Em cenários de RM (mensagens confiáveis seguras), os ataques de reflexo são mitigados porque:  
  
- Os esquemas de mensagem de resposta Create Sequence e Create Sequence são diferentes.  
  
- Para sequências simplex, as mensagens de sequência que o cliente envia não podem ser reproduzidas para ele porque o cliente não pode entender essas mensagens.  
  
- Para sequências duplex, as duas IDs de sequência devem ser exclusivas. Portanto, uma mensagem de sequência de saída não pode ser repetida como uma mensagem de sequência de entrada (todos os cabeçalhos e corpos de sequência também são assinados).  
  
 As únicas associações que são suscetíveis a ataques de reflexão são aquelas sem WS-Addressing: associações personalizadas que têm WS-Addressing desabilitadas e usam a segurança baseada em chave simétrica. O <xref:System.ServiceModel.BasicHttpBinding> não usa WS-Addressing por padrão, mas não usa a segurança baseada em chave simétrica de forma a permitir que ela fique vulnerável a esse ataque.  
  
 A mitigação de associações personalizadas é não estabelecer o contexto de segurança ou exigir WS-Addressing cabeçalhos.  
  
## <a name="web-farm-attacker-replays-request-to-multiple-nodes"></a>Web farm: o invasor repete a solicitação para vários nós  

 Um cliente usa um serviço que é implementado em um Web farm. Um invasor repete uma solicitação que foi enviada para um nó no farm para outro nó no farm. Além disso, se um serviço for reiniciado, o cache de reprodução será liberado, permitindo que um invasor reproduza a solicitação. (O cache contém os valores de assinatura de mensagem usados anteriormente e que impede as repetições para que essas assinaturas possam ser usadas apenas uma vez. Os caches de reprodução não são compartilhados em um Web farm.)  
  
 Atenuantes incluem:  
  
- Use a segurança do modo de mensagem com tokens de contexto de segurança com estado (com ou sem conversa segura habilitada). Para obter mais informações, consulte [como: criar um token de contexto de segurança para uma sessão segura](how-to-create-a-security-context-token-for-a-secure-session.md).  
  
- Configure o serviço para usar a segurança em nível de transporte.  
  
## <a name="see-also"></a>Consulte também

- [Considerações sobre segurança](security-considerations-in-wcf.md)
- [Divulgação de Informações Confidenciais](information-disclosure.md)
- [Elevação de Privilégio](elevation-of-privilege.md)
- [Negação de Serviço](denial-of-service.md)
- [Adulteração](tampering.md)
- [Cenários sem suporte](unsupported-scenarios.md)
