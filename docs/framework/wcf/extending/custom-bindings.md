---
description: 'Saiba mais sobre: associações personalizadas'
title: Associações personalizadas
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, endpoints
- Windows Communication Foundation, configuration
ms.assetid: 58532b6d-4eea-4a4f-854f-a1c8c842564d
ms.openlocfilehash: ced0f9ada7238b43216a246d75dd391aa6eb3f2b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735342"
---
# <a name="custom-bindings"></a>Associações personalizadas

Você pode usar a <xref:System.ServiceModel.Channels.CustomBinding> classe quando uma das associações fornecidas pelo sistema não atender aos requisitos do seu serviço. Todas as associações são construídas a partir de um conjunto ordenado de elementos de associação. Associações personalizadas podem ser criadas a partir de um conjunto de elementos de associação fornecidos pelo sistema ou podem incluir elementos de associação personalizados definidos pelo usuário. Você pode usar elementos de associação personalizados, por exemplo, para habilitar o uso de novos transportes ou codificadores em um ponto de extremidade de serviço. Para obter exemplos de funcionamento, consulte [exemplos de associação personalizada](/previous-versions/dotnet/netframework-3.5/ms751479(v=vs.90)). Para obter mais informações, confira [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md).

## <a name="construction-of-a-custom-binding"></a>Construção de uma associação personalizada

Uma associação personalizada é criada usando o <xref:System.ServiceModel.Channels.CustomBinding.%23ctor%2A> Construtor de uma coleção de elementos de associação que são "empilhados" em uma ordem específica:

- Na parte superior, há uma <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> classe opcional que permite transações de fluxo.

- A seguir é uma <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> classe opcional que fornece um mecanismo de sessão e ordenação, conforme definido na especificação de WS-ReliableMessaging. Uma sessão pode cruzar o SOAP e transportar intermediários.

- A seguir é uma <xref:System.ServiceModel.Channels.SecurityBindingElement> classe opcional que fornece recursos de segurança como autorização, autenticação, proteção e confidencialidade.

- A seguir é uma <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> classe opcional que fornece a capacidade de ter duas vias de comunicação duplex com um protocolo de transporte que não ofereça suporte à comunicação duplex nativamente, como http.

- A seguir é uma <xref:System.ServiceModel.Channels.OneWayBindingElement> classe opcional) que fornece comunicação unidirecional.

- A seguir é um elemento de associação de segurança de fluxo opcional que pode ser um dos seguintes.

  - <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>

  - <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>

- A seguir está um elemento de associação de codificação de mensagem necessário. Você pode usar seu próprio codificador de mensagem ou uma das três associações de codificação de mensagem:

  - <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>

  - <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>

  - <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>

Na parte inferior, há um elemento Transport necessário. Você pode usar seu próprio transporte ou um dos seguintes elementos de ligação de transporte Windows Communication Foundation (WCF) fornece:

- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>

- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>

- <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>

- <xref:System.ServiceModel.Channels.PeerTransportBindingElement>

- <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>

- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBindingElement>

- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>

A tabela a seguir resume as opções para cada camada.

|Camada|Opções|Obrigatório|
|-----------|-------------|--------------|
|Transactions|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement>|Não|
|Confiabilidade|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement>|Não|
|Segurança|<xref:System.ServiceModel.Channels.SecurityBindingElement>|Não|
|Codificação|Texto, binário, mecanismo de otimização de transmissão de mensagens (MTOM), personalizado|Yes|
|Transport|TCP, HTTP, HTTPS, pipes nomeados (também conhecido como IPC), ponto a ponto (P2P), Enfileiramento de mensagens (também conhecido como MSMQ), personalizado|Yes|

Além disso, você pode definir seus próprios elementos de ligação e inseri-los entre as camadas definidas anteriormente.

## <a name="see-also"></a>Consulte também

- [Visão geral de criação de ponto de extremidade](../endpoint-creation-overview.md)
- [Usando associações para configurar serviços e clientes](../using-bindings-to-configure-services-and-clients.md)
- [Associações fornecidas pelo sistema](../system-provided-bindings.md)
- [Como: personalizar uma associação fornecida pelo sistema](how-to-customize-a-system-provided-binding.md)
- [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md)
- [Associação personalizado](../samples/custom-binding.md)
