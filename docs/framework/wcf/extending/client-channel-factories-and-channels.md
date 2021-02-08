---
description: 'Saiba mais sobre: cliente: fábricas de canal e canais'
title: 'Cliente: fábricas de canais e canais'
ms.date: 03/30/2017
ms.assetid: ef245191-fdab-4468-a0da-7c6f25d2110f
ms.openlocfilehash: b61c37743899b8ba74ec18cc84397e4521e7bde7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803029"
---
# <a name="client-channel-factories-and-channels"></a>Cliente: fábricas de canais e canais

Este tópico discute a criação de fábricas de canais e canais.  
  
## <a name="channel-factories-and-channels"></a>fábricas de canais e canais  

 As fábricas de canal são responsáveis pela criação de canais. Os canais criados por fábricas de canal são usados para enviar mensagens. Esses canais são responsáveis por obter a mensagem da camada acima, executar qualquer processamento necessário e, em seguida, enviar a mensagem para a camada abaixo. O gráfico a seguir ilustra esse processo.  
  
 ![Fábricas de cliente e canais](./media/wcfc-wcfchannelsigure2highlevelfactgoriesc.gif "wcfc_WCFChannelsigure2HIghLevelFactgoriesc")  
Uma fábrica de canais cria canais.  
  
 Quando fechado, as fábricas de canal são responsáveis por fechar todos os canais criados que ainda não estão fechados. Observe que o modelo é assimétrico aqui porque, quando um ouvinte de canal é fechado, ele só para de aceitar novos canais, mas deixa os canais existentes abertos para que possam continuar recebendo mensagens.  
  
 O WCF fornece auxiliares de classe base para esse processo. (Para obter um diagrama das classes auxiliares de canal abordadas neste tópico, consulte [visão geral do modelo de canal](channel-model-overview.md).)  
  
- A <xref:System.ServiceModel.Channels.CommunicationObject> classe implementa <xref:System.ServiceModel.ICommunicationObject> e impõe a máquina de estado descrita na etapa 2 de [desenvolvimento de canais](developing-channels.md).  
  
- A <xref:System.ServiceModel.Channels.ChannelManagerBase> classe implementa <xref:System.ServiceModel.Channels.CommunicationObject> e fornece uma classe base unificada para o <xref:System.ServiceModel.Channels.ChannelFactoryBase?displayProperty=nameWithType> e o <xref:System.ServiceModel.Channels.ChannelListenerBase?displayProperty=nameWithType> . A <xref:System.ServiceModel.Channels.ChannelManagerBase> classe funciona em conjunto com <xref:System.ServiceModel.Channels.ChannelBase> , que é uma classe base que implementa <xref:System.ServiceModel.Channels.IChannel> .
  
- A <xref:System.ServiceModel.Channels.ChannelFactoryBase> classe implementa <xref:System.ServiceModel.Channels.ChannelManagerBase> e <xref:System.ServiceModel.Channels.IChannelFactory> consolida as `CreateChannel` sobrecargas em um `OnCreateChannel` método abstrato.
  
- A <xref:System.ServiceModel.Channels.ChannelListenerBase> classe implementa <xref:System.ServiceModel.Channels.IChannelListener> . Ele cuida do gerenciamento de estado básico.
  
 A discussão a seguir se baseia no exemplo de [transporte: UDP](../samples/transport-udp.md) .  
  
### <a name="creating-a-channel-factory"></a>Criando uma fábrica de canais  

 O `UdpChannelFactory` deriva de <xref:System.ServiceModel.Channels.ChannelFactoryBase> . As substituições de exemplo <xref:System.ServiceModel.Channels.ChannelFactoryBase.GetProperty%2A> para fornecer acesso à versão de mensagem do codificador de mensagem. O exemplo também substitui <xref:System.ServiceModel.Channels.ChannelFactoryBase.OnClose%2A> para subdividir nossa instância de <xref:System.ServiceModel.Channels.BufferManager> quando a máquina de estado faz a transição.  
  
#### <a name="the-udp-output-channel"></a>O canal de saída UDP  

 O `UdpOutputChannel` implementa <xref:System.ServiceModel.Channels.IOutputChannel> . O Construtor valida os argumentos e constrói um objeto de destino <xref:System.Net.EndPoint> com base no <xref:System.ServiceModel.EndpointAddress> que é passado.  
  
 A substituição de <xref:System.ServiceModel.Channels.CommunicationObject.OnOpen%2A> cria um soquete que é usado para enviar mensagens para isso <xref:System.Net.EndPoint> .  
  
 ```csharp
this.socket = new Socket(  
this.remoteEndPoint.AddressFamily,
   SocketType.Dgram,
   ProtocolType.Udp
);  
```  

 O canal pode ser fechado de forma normal ou inadequada. Se o canal for fechado normalmente, o Soquete será fechado e uma chamada será feita ao método da classe base `OnClose` . Se isso lançar uma exceção, a infraestrutura chamará `Abort` para garantir que o canal seja limpo.  
  
```csharp  
this.socket.Close();  
base.OnClose(timeout);  
```  
  
 Implemente `Send()` e `BeginSend()` / `EndSend()` . Isso é dividido em duas seções principais. Primeiro, Serialize a mensagem em uma matriz de bytes:  
  
```csharp  
ArraySegment<byte> messageBuffer = EncodeMessage(message);  
```  
  
 Em seguida, envie os dados resultantes na conexão:  
  
```csharp  
this.socket.SendTo(  
  messageBuffer.Array,
  messageBuffer.Offset,
  messageBuffer.Count,
  SocketFlags.None,
  this.remoteEndPoint  
);  
```  
  
## <a name="see-also"></a>Consulte também

- [Canais de desenvolvimento](developing-channels.md)
