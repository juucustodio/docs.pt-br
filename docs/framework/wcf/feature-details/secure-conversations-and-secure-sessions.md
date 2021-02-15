---
description: 'Saiba mais sobre: conversas seguras e sessões seguras'
title: Sessões seguras e conversas seguras
ms.date: 03/30/2017
ms.assetid: 48cb104a-532d-40ae-aa57-769dae103fda
ms.openlocfilehash: dd935fd5de833dc2ba68b1aec3a2992dcba6a000
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99733106"
---
# <a name="secure-conversations-and-secure-sessions"></a>Sessões seguras e conversas seguras

Um recurso do Windows Communication Foundation (WCF) é a capacidade de estabelecer sessões seguras entre dois pontos de extremidade que se autenticam e concordam com um processo de criptografia e assinatura digital. Por exemplo, o ponto de extremidade de serviço pode exigir um ponto de extremidade de cliente para enviar um token de segurança com base em um certificado X. 509 para autenticação. Depois que o cliente é autenticado, o ponto de extremidade de serviço retorna um identificador de contexto de segurança (SCT) de volta para o cliente que é usado para proteger todas as mensagens subsequentes na sessão. O estabelecimento dessa sessão segura permite que o conjunto de mensagens trocadas entre os dois pontos de extremidade seja mais eficiente, pois o SCT tem uma chave simétrica. As chaves assimétricas, nas quais os certificados X. 509 se baseiam, exigem uma capacidade de computação significativamente maior do que as chaves simétricas ao gerar uma assinatura digital ou criptografar um conjunto de dados.  
  
 A política de bootstrap (definida na seção 6.2.7 do padrão [WS-SecurityPolicy](https://docs.oasis-open.org/ws-sx/ws-securitypolicy/200702/ws-securitypolicy-1.2-spec-os.html) ) contém as asserções de segurança de mensagem usadas para proteger o canal e autenticar o cliente antes do RST/SCT e da troca de RSTR/SCT. Certas associações padrão do WCF têm uma `Security.Message.EstablishSecurityContext` propriedade que controla se a conversa segura é usada. Ao usar associações personalizadas, a inicialização é indicada por meio do aninhamento de elementos de associação de segurança, por meio do [\<secureConversationBootstrap>](../../configure-apps/file-schema/wcf/secureconversationbootstrap.md) no arquivo de configuração ou chamando <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%2A> no código.  
  
 Para obter mais informações sobre sessões, consulte [usando sessões](../using-sessions.md).  
  
## <a name="see-also"></a>Consulte também

- [Sessões,instanciação e simultaneidade](sessions-instancing-and-concurrency.md)
- [Como: criar um serviço que requer sessões](how-to-create-a-service-that-requires-sessions.md)
