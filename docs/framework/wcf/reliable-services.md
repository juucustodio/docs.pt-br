---
description: 'Saiba mais sobre: Reliable Services'
title: Serviços confiáveis
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], reliable messaging
- Windows Communication Foundation [WCF], reliable messaging
- WCF [WCF], reliable sessions
- Windows Communication Foundation [WCF], reliable sessions
- service contracts [WCF], reliable services
ms.assetid: 07814ed0-0775-47f2-987b-d8134fdd5099
ms.openlocfilehash: c38f949e57b1891da2433875571443656c7044dd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99779199"
---
# <a name="reliable-services"></a>Serviços confiáveis

As filas e as sessões confiáveis são os recursos de Windows Communication Foundation (WCF) que implementam mensagens confiáveis. Este tópico explica os recursos de mensagens confiáveis do WCF.  
  
 O *sistema de mensagens confiável* é como uma fonte de mensagens confiável (chamada de *origem*) transfere mensagens de forma confiável para um destino de mensagem confiável (chamado de *destino*).  
  
 O sistema de mensagens confiável executa as seguintes funções:  
  
- Transfere garantias de mensagens enviadas de uma origem para um destino, independentemente da transferência de mensagens ou falhas de transporte.  
  
- Separa a origem e o destino entre si. Isso fornece falha independente e recuperação da origem e do destino, bem como transferência confiável e entrega de mensagens, mesmo quando a origem ou o destino não está disponível.  
  
 As mensagens confiáveis frequentemente são o custo de alta latência. *Latência* é o tempo que leva para a mensagem alcançar o destino da origem. O WCF, portanto, fornece os seguintes tipos de mensagens confiáveis:  
  
- [Sessões confiáveis](./feature-details/reliable-sessions.md), que oferecem transferência confiável sem o custo de alta latência.  
  
- [Filas no WCF](./feature-details/queues-in-wcf.md), que oferece transferências confiáveis e separação entre a origem e o destino.  
  
## <a name="reliable-sessions"></a>Sessões confiáveis  

 As sessões confiáveis fornecem transferência de mensagens confiável de ponta a ponta entre uma origem e um destino usando o protocolo WS-Reliable de mensagens, independentemente do número ou tipo de intermediários que separam os pontos de extremidade de mensagens (origem e destino). Isso inclui os intermediários de transporte que não usam SOAP (por exemplo, proxies HTTP) ou intermediários que usam SOAP (por exemplo, roteadores ou pontes baseados em SOAP) que são necessários para que as mensagens fluam entre os pontos de extremidade. As sessões confiáveis usam uma janela de transferência na memória para mascarar falhas de nível de mensagem SOAP e restabelecer conexões no caso de falhas de transporte.  
  
 As sessões confiáveis fornecem transferências de mensagens confiáveis de baixa latência. Eles fornecem mensagens SOAP sobre quaisquer proxies ou intermediários, equivalentes ao que o TCP fornece para pacotes em pontes IP. Para obter mais informações sobre sessões confiáveis, consulte [sessões confiáveis](./feature-details/reliable-sessions.md).  
  
### <a name="queues"></a>Filas  

 As filas no WCF fornecem transferências confiáveis de mensagens e separação entre origens e destinos ao custo de alta latência. A comunicação na fila do WCF é criada com base no MSMQ (enfileiramento de mensagens).  
  
 O MSMQ é fornecido como um componente opcional com o Windows. O serviço MSMQ é executado como um serviço do Windows. Ele captura mensagens para transmissão em uma fila de transmissão em nome da origem e a entrega a uma fila de destino. A fila de destino aceita mensagens em nome do destino para entrega posterior sempre que o destino solicita mensagens. Os gerenciadores MSMQ implementam um protocolo de transferência de mensagens confiável para que as mensagens não sejam perdidas na transmissão. O protocolo pode ser nativo ou um protocolo baseado em SOAP chamado de SRMP (protocolo de mensagens confiáveis SOAP).  
  
 A separação, combinada com transferências de mensagens confiáveis entre filas, permite que os aplicativos que são livremente acoplados se comuniquem de forma confiável. Ao contrário de sessões confiáveis, a origem e o destino não precisam estar em execução ao mesmo tempo. Isso habilita implicitamente cenários em que as filas são, na verdade, usadas como um mecanismo de nivelamento de carga quando a taxa de produção de mensagem da origem e a taxa de destino do consumo de mensagem não coincidem. Para obter mais informações sobre filas, consulte [filas no WCF](./feature-details/queues-in-wcf.md).  
  
## <a name="see-also"></a>Consulte também

- [Visão geral de sessões confiáveis](./feature-details/reliable-sessions-overview.md)
- [Enfileiramento no WCF](./feature-details/queuing-in-wcf.md)
