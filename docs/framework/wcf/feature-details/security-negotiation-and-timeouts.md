---
description: 'Saiba mais sobre: negociação de segurança e tempos limite'
title: Negociação de segurança e tempo limite
ms.date: 03/30/2017
ms.assetid: 02a428f1-84e5-4d28-a11f-53ce31d63196
ms.openlocfilehash: 50055698f9a9946d0c0110a964cf9ce5b9f4fa28
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99632432"
---
# <a name="security-negotiation-and-timeouts"></a>Negociação de segurança e tempo limite

Quando os clientes e serviços são autenticados, Windows Communication Foundation (WCF) dá suporte a um modo em que a credencial de serviço é negociada como parte da autenticação. Nesses cenários, uma troca potencialmente de vários trechos ocorre entre o cliente e o serviço para propagar a credencial de serviço para o cliente. A <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NegotiationTimeout%2A> propriedade controla por quanto tempo a troca de vários trechos pode levar para ser concluída. No entanto, esse tempo limite só se aplica se o Exchange realmente demorar mais que uma única solicitação-resposta. Nos casos em que a negociação é concluída em uma única viagem de ida e volta, o tempo limite não se aplica.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
- [Como: definir a distorção máxima do relógio](how-to-set-a-max-clock-skew.md)
