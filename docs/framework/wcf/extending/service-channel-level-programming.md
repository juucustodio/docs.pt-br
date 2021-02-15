---
description: 'Saiba mais sobre: programação de Channel-Level de serviço'
title: Programação de nível por canal de serviço
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8d8dcd85-0a05-4c44-8861-4a0b3b90cca9
ms.openlocfilehash: 9d89b073430ccdf80bdcbdfc50fd1e002fc807ff
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644054"
---
# <a name="service-channel-level-programming"></a>Programação de nível por canal de serviço

Este tópico descreve como gravar um aplicativo de serviço do Windows Communication Foundation (WCF) sem usar o <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> e seu modelo de objeto associado.  
  
## <a name="receiving-messages"></a>recebendo mensagens  

 Para estar pronto para receber e processar mensagens, as etapas a seguir são necessárias:  
  
1. Crie uma associação.  
  
2. Crie um ouvinte de canal.  
  
3. Abra o ouvinte do canal.  
  
4. Leia a solicitação e envie uma resposta.  
  
5. Feche todos os objetos de canal.  
  
#### <a name="creating-a-binding"></a>Criar uma associação  

 A primeira etapa na escuta e no recebimento de mensagens é a criação de uma associação. O WCF é fornecido com várias associações internas ou fornecidas pelo sistema que podem ser usadas diretamente por meio da criação de uma instância de uma delas. Além disso, você também pode criar sua própria associação personalizada instanciando uma classe Personalizadabinding que é o que o código na Listagem 1 faz.  
  
 O exemplo de código a seguir cria uma instância do <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> e adiciona um <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType> à sua coleção Elements, que é uma coleção de elementos Binding que são usados para criar a pilha de canais. Neste exemplo, como a coleção Elements tem apenas o <xref:System.ServiceModel.Channels.HttpTransportBindingElement> , a pilha de canais resultante tem apenas o canal de transporte http.  
  
#### <a name="building-a-channellistener"></a>Criando um ChannelListener  

 Depois de criar uma associação, chamamos <xref:System.ServiceModel.Channels.Binding.BuildChannelListener%2A?displayProperty=nameWithType> para criar o ouvinte de canal em que o parâmetro de tipo é a forma de canal a ser criada. Neste exemplo, estamos usando <xref:System.ServiceModel.Channels.IReplyChannel?displayProperty=nameWithType> porque desejamos escutar mensagens de entrada em um padrão de troca de mensagens de solicitação/resposta.  
  
 <xref:System.ServiceModel.Channels.IReplyChannel> é usado para receber mensagens de solicitação e enviar mensagens de resposta de retorno. Chamar <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A?displayProperty=nameWithType> retorna um <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType> , que pode ser usado para receber a mensagem de solicitação e para enviar de volta uma mensagem de resposta.  
  
 Ao criar o ouvinte, passamos o endereço de rede no qual ele escuta, nesse caso `http://localhost:8080/channelapp` . Em geral, cada canal de transporte dá suporte a um ou possivelmente vários esquemas de endereço, por exemplo, o transporte HTTP dá suporte a esquemas http e HTTPS.  
  
 Também passamos um vazio <xref:System.ServiceModel.Channels.BindingParameterCollection?displayProperty=nameWithType> ao criar o ouvinte. Um parâmetro de associação é um mecanismo para passar parâmetros que controlam como o ouvinte deve ser compilado. Em nosso exemplo, não estamos usando nenhum desses parâmetros, portanto, passamos uma coleção vazia.  
  
#### <a name="listening-for-incoming-messages"></a>Escutando mensagens de entrada  

 Em seguida, chamamos <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> o ouvinte e começamos a aceitar canais. O comportamento do <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A?displayProperty=nameWithType> depende se o transporte é orientado a conexão ou sem conexão. Para Transportações orientadas a conexão, os <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A> blocos até que uma nova solicitação de conexão seja recebida no ponto em que ele retorna um novo canal que representa essa nova conexão. Para transportes sem conexão, como HTTP, <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A> retorna imediatamente com o único e o canal que o ouvinte de transporte cria.  
  
 Neste exemplo, o ouvinte retorna um canal que implementa <xref:System.ServiceModel.Channels.IReplyChannel> . Para receber mensagens nesse canal, primeiro chamamos isso <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> para colocá-lo em um estado pronto para comunicação. Em seguida, chamamos <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A> os blocos até que uma mensagem chegue.  
  
#### <a name="reading-the-request-and-sending-a-reply"></a>Lendo a solicitação e enviando uma resposta  

 Quando <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A> retorna um <xref:System.ServiceModel.Channels.RequestContext> , obtemos a mensagem recebida usando sua <xref:System.ServiceModel.Channels.RequestContext.RequestMessage%2A> propriedade. Escrevemos a ação da mensagem e o conteúdo do corpo, (que supomos que é uma cadeia de caracteres).  
  
 Para enviar uma resposta, criamos uma nova mensagem de resposta nesse caso, passando os dados de cadeia de caracteres que recebemos na solicitação. Em seguida, chamamos <xref:System.ServiceModel.Channels.RequestContext.Reply%2A> para enviar a mensagem de resposta.  
  
#### <a name="closing-objects"></a>Fechando objetos  

 Para evitar vazamento de recursos, é muito importante fechar objetos usados na comunicação quando eles não são mais necessários. Neste exemplo, fechamos a mensagem de solicitação, o contexto da solicitação, o canal e o ouvinte.  
  
 O exemplo de código a seguir mostra um serviço básico no qual um ouvinte de canal recebe apenas uma mensagem. Um serviço real continua aceitando canais e recebendo mensagens até que o serviço saia.  
  
 [!code-csharp[ChannelProgrammingBasic#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/channelprogrammingbasic/cs/serviceprogram.cs#1)]
 [!code-vb[ChannelProgrammingBasic#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelprogrammingbasic/vb/serviceprogram.vb#1)]
