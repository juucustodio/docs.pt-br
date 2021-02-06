---
description: 'Saiba mais sobre: sessões confiáveis'
title: Sessões confiáveis
ms.date: 03/30/2017
f1_keywords:
- Windows Communication Foundation, sessions and instances
- WCF, sessions and instances
- sessions and instances [WCF]
helpviewer_keywords:
- instances [WCF]
- sessions [WCF]
ms.assetid: 143951b3-3aa0-4540-b4b7-d33e77e874a1
ms.openlocfilehash: 86df4ccf9c1fd52d162ad7272ece5591f0ca7482
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99632874"
---
# <a name="reliable-sessions"></a>Sessões confiáveis

Esta seção descreve o que é uma sessão confiável do Windows Communication Foundation (WCF), para que ela é usada, como e quando usar uma delas, quais configurações de ligação dão suporte a ela e ponteiros sobre as práticas recomendadas. A tabela a seguir resume os detalhes sobre os pontos essenciais e tópicos relacionados nesta seção.

O WCF de sessão confiável fornece recursos que garantem que as mensagens enviadas entre os pontos de extremidade sejam transferidas entre intermediários de transporte ou SOAP e são entregues apenas uma vez e, opcionalmente, na mesma ordem em que foram enviadas.

Para usar uma sessão confiável com um aplicativo WCF, use uma das associações fornecidas pelo sistema no WCF que ofereçam suporte a uma sessão confiável por padrão ou como uma opção, ou crie sua própria associação personalizada que dê suporte à sessão.

## <a name="in-this-section"></a>Nesta seção

[Visão geral de sessões confiáveis](reliable-sessions-overview.md) Descreve as sessões confiáveis, quando usá-las, as diferentes associações que dão suporte a sessões confiáveis e como elas funcionam.

[Como: trocar mensagens em uma sessão confiável](how-to-exchange-messages-within-a-reliable-session.md) Descreve como criar uma sessão confiável via HTTP usando uma associação personalizada especificada na configuração.

[Como: proteger mensagens em sessões confiáveis](how-to-secure-messages-within-reliable-sessions.md) Descreve como proteger uma sessão confiável.

[Como: criar uma associação de sessão confiável personalizada com HTTPS](how-to-create-a-custom-reliable-session-binding-with-https.md) Descreve como criar uma sessão confiável por HTTPS.

[Práticas recomendadas para sessões confiáveis](best-practices-for-reliable-sessions.md) Descreve algumas das práticas recomendadas associadas ao uso de uma sessão confiável.

## <a name="reference"></a>Referência

<xref:System.ServiceModel.ReliableSession>

## <a name="see-also"></a>Consulte também

- [Sessões confiáveis e filas](queues-and-reliable-sessions.md)
- [Sessões,instanciação e simultaneidade](sessions-instancing-and-concurrency.md)
