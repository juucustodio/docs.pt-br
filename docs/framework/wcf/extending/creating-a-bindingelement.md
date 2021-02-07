---
description: 'Saiba mais sobre: Criando um BindingElement'
title: Criando um BindingElement
ms.date: 03/30/2017
ms.assetid: 01a35307-a41f-4ef6-a3db-322af40afc99
ms.openlocfilehash: de5ef045f2e83985cabd36c53652d46536889fa2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735420"
---
# <a name="creating-a-bindingelement"></a>Criando um BindingElement

Associações e elementos de associação (objetos que estendem <xref:System.ServiceModel.Channels.Binding?displayProperty=nameWithType> e <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> , respectivamente) são o local em que o modelo de aplicativo Windows Communication Foundation (WCF) está associado a fábricas de canal e ouvintes de canal. Sem associações, o uso de canais personalizados requer programação no nível do canal, conforme descrito em programação de [Channel-Level de serviço](service-channel-level-programming.md) e programação de [Channel-Level de cliente](client-channel-level-programming.md). Este tópico discute o requisito mínimo para habilitar o uso do canal no WCF, o desenvolvimento de um <xref:System.ServiceModel.Channels.BindingElement> para seu canal e a habilitação do uso do aplicativo, conforme descrito na etapa 4 do [desenvolvimento de canais](developing-channels.md).  
  
## <a name="overview"></a>Visão geral  

 A criação de um <xref:System.ServiceModel.Channels.BindingElement> para seu canal permite que os desenvolvedores o usem em um aplicativo WCF. <xref:System.ServiceModel.Channels.BindingElement> os objetos podem ser usados da <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> classe para conectar um aplicativo WCF ao seu canal sem ter que obter as informações de tipo precisas de seu canal.  
  
 Depois que um <xref:System.ServiceModel.Channels.BindingElement> tiver sido criado, você poderá habilitar mais funcionalidade, dependendo dos requisitos, seguindo as etapas de desenvolvimento de canal restantes descritas em [desenvolvimento de canais](developing-channels.md).  
  
## <a name="adding-a-binding-element"></a>Adicionando um elemento de associação  

 Para implementar um personalizado <xref:System.ServiceModel.Channels.BindingElement> , escreva uma classe que herde de <xref:System.ServiceModel.Channels.BindingElement> . Por exemplo, se você tiver desenvolvido um `ChunkingChannel` que pode dividir mensagens grandes em partes e remontá-las na outra extremidade, poderá usar esse canal em qualquer associação implementando um <xref:System.ServiceModel.Channels.BindingElement> e configurando a associação para usá-lo. O restante deste tópico usa o `ChunkingChannel` como um exemplo para demonstrar os requisitos de implementação de um elemento de associação.  
  
 Um `ChunkingBindingElement` é responsável por criar o `ChunkingChannelFactory` e o `ChunkingChannelListener` . Ele substitui <xref:System.ServiceModel.Channels.BindingElement.CanBuildChannelFactory%2A> e <xref:System.ServiceModel.Channels.BindingElement.CanBuildChannelListener%2A> implementa e verifica se o parâmetro de tipo é <xref:System.ServiceModel.Channels.IDuplexSessionChannel> (em nosso exemplo, essa é a única forma de canal com suporte no `ChunkingChannel` ) e se os outros elementos de ligação na associação dão suporte a essa forma de canal.  
  
 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> primeiro verifica se a forma de canal solicitada pode ser criada e, em seguida, obtém uma lista de ações de mensagens a serem enfileiradas. Em seguida, ele cria um novo `ChunkingChannelFactory` , passando-o para a fábrica de canais interna. (Se você estiver criando um elemento de associação de transporte, esse elemento será o último na pilha de associação e, portanto, deverá criar um ouvinte de canal ou fábrica de canais.)  
  
 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> o tem uma implementação semelhante para criar `ChunkingChannelListener` e passar o ouvinte de canal interno.  
  
 Como outro exemplo que usa um canal de transporte, o exemplo [Transport: UDP](../samples/transport-udp.md) fornece a substituição a seguir.  
  
 No exemplo, o elemento de associação é `UdpTransportBindingElement` , que deriva de <xref:System.ServiceModel.Channels.TransportBindingElement> . Ele substitui os métodos a seguir para criar as fábricas associadas ao canal.  
  
```csharp  
public IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
{  
    return (IChannelFactory<TChannel>)(object)new UdpChannelFactory(this, context);  
}  
  
public IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
{  
    return (IChannelListener<TChannel>)(object)new UdpChannelListener(this, context);  
}  
```  
  
 Ele também contém membros para clonar `BindingElement` e retornar nosso esquema (SOAP. UDP).  
  
#### <a name="protocol-binding-elements"></a>Elementos de associação de protocolo  

 Novos elementos de associação podem substituir ou aumentar qualquer um dos elementos de associação incluídos, adicionando novos transportes, codificações ou protocolos de nível superior. Para criar um novo elemento de associação de protocolo, comece estendendo a <xref:System.ServiceModel.Channels.BindingElement> classe. No mínimo, você deve implementar o <xref:System.ServiceModel.Channels.BindingElement.Clone%2A?displayProperty=nameWithType> e implementar o usando o `ChannelProtectionRequirements` <xref:System.ServiceModel.Channels.IChannel.GetProperty%2A?displayProperty=nameWithType> . Isso retorna o <xref:System.ServiceModel.Security.ChannelProtectionRequirements> para esse elemento de associação.  Para obter mais informações, consulte <xref:System.ServiceModel.Security.ChannelProtectionRequirements>.  
  
 <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> deve retornar uma cópia nova desse elemento de associação. Como prática recomendada, recomendamos que os autores de elemento de associação implementem <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> usando um construtor de cópia que chama o construtor de cópia base e, em seguida, clona quaisquer campos adicionais nessa classe.  
  
#### <a name="transport-binding-elements"></a>Elementos de associação de transporte  

 Para criar um novo elemento de associação de transporte, estenda a <xref:System.ServiceModel.Channels.TransportBindingElement> interface. No mínimo, você deve implementar o <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> método e a <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A?displayProperty=nameWithType> propriedade.  
  
 <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> – Deve retornar uma cópia nova desse elemento de associação.  Como prática recomendada, recomendamos que os autores de elemento de associação implementem clone por meio de um construtor de cópia que chama o construtor de cópia base e, em seguida, clona quaisquer campos adicionais nessa classe.  
  
 <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> – A <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> propriedade Get retorna o esquema de URI para o protocolo de transporte representado pelo elemento Binding. Por exemplo, o <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType> e o <xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=nameWithType> retornam "http" e "net. TCP" de suas respectivas <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> Propriedades.  
  
#### <a name="encoding-binding-elements"></a>Codificando elementos de associação  

 Para criar novos elementos de associação de codificação, comece estendendo a <xref:System.ServiceModel.Channels.BindingElement> classe e implementando a <xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=nameWithType> classe. No mínimo, você deve implementar os <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A?displayProperty=nameWithType> métodos, e a <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.MessageVersion%2A?displayProperty=nameWithType> propriedade.  
  
- <xref:System.ServiceModel.Channels.BindingElement.Clone%2A>. Retorna uma nova cópia desse elemento de associação. Como prática recomendada, recomendamos que os autores de elemento de associação implementem <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> usando um construtor de cópia que chama o construtor de cópia base e, em seguida, clona quaisquer campos adicionais nessa classe.  
  
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A>. Retorna um <xref:System.ServiceModel.Channels.MessageEncoderFactory> , que fornece um identificador para a classe real que implementa o novo codificador e que deve ser estendido <xref:System.ServiceModel.Channels.MessageEncoder> . Para obter mais informações, consulte <xref:System.ServiceModel.Channels.MessageEncoderFactory> e <xref:System.ServiceModel.Channels.MessageEncoder>.  
  
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.MessageVersion%2A>. Retorna o <xref:System.ServiceModel.Channels.MessageVersion> usado nessa codificação, que representa as versões de SOAP e WS-Addressing em uso.  
  
 Para obter uma lista completa de métodos e propriedades opcionais para elementos de associação de codificação definidos pelo usuário, consulte <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> .  
  
 Para obter mais informações sobre como criar um novo elemento de associação, consulte [Criando associações de User-Defined](creating-user-defined-bindings.md).  
  
 Depois de criar um elemento de associação para seu canal, retorne ao tópico [desenvolvendo canais](developing-channels.md) para ver se você deseja adicionar suporte ao arquivo de configuração ao seu elemento de associação, se e como adicionar suporte à publicação de metadados e se e como construir uma associação definida pelo usuário que usa seu elemento de associação.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.BindingElement>
- [Canais de desenvolvimento](developing-channels.md)
- [Transporte: UDP](../samples/transport-udp.md)
