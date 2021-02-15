---
description: 'Saiba mais sobre: programação de Channel-Level de cliente'
title: Programação de nível de canal cliente
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3b787719-4e77-4e77-96a6-5b15a11b995a
ms.openlocfilehash: 7e4e977231339fbbede7111e38a67054eb24eed9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802990"
---
# <a name="client-channel-level-programming"></a>Programação de nível de canal cliente

Este tópico descreve como gravar um aplicativo cliente do Windows Communication Foundation (WCF) sem usar a <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType> classe e seu modelo de objeto associado.  
  
## <a name="sending-messages"></a>enviando mensagens  

 Para estar pronto para enviar mensagens e receber e processar respostas, as etapas a seguir são necessárias:  
  
1. Crie uma associação.  
  
2. Crie uma fábrica de canais.  
  
3. Criar um canal.  
  
4. Envie uma solicitação e leia a resposta.  
  
5. Feche todos os objetos de canal.  
  
#### <a name="creating-a-binding"></a>Criar uma associação  

 Semelhante ao caso de recebimento (consulte [programação de Channel-Level de serviço](service-channel-level-programming.md)), o envio de mensagens começa pela criação de uma associação. Este exemplo cria um novo <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> e adiciona um <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType> à sua coleção de elementos.  
  
#### <a name="building-a-channelfactory"></a>Criando uma ChannelFactory  

 Em vez de criar um <xref:System.ServiceModel.Channels.IChannelListener?displayProperty=nameWithType> , desta vez, criamos um <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> chamando <xref:System.ServiceModel.ChannelFactory.CreateFactory%2A?displayProperty=nameWithType> na associação em que o parâmetro de tipo é <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType> . Enquanto ouvintes de canal são usados pelo lado que aguarda mensagens de entrada, as fábricas de canal são usadas pelo lado que inicia a comunicação para criar um canal. Assim como ouvintes de canal, as fábricas de canal devem ser abertas primeiro antes de poderem ser usadas.  
  
#### <a name="creating-a-channel"></a>Criando um canal  

 Em seguida, chamamos <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> para criar um <xref:System.ServiceModel.Channels.IRequestChannel> . Essa chamada pega o endereço do ponto de extremidade com o qual desejamos se comunicar usando o novo canal que está sendo criado. Assim que tivermos um canal, chamamos o Open nele para colocá-lo em um estado pronto para comunicação. Dependendo da natureza do transporte, essa chamada para Open pode iniciar uma conexão com o ponto de extremidade de destino ou pode não fazer nada na rede.  
  
#### <a name="sending-a-request-and-reading-the-reply"></a>Enviando uma solicitação e lendo a resposta  

 Uma vez que temos um canal aberto, podemos criar uma mensagem e usar o método de solicitação do canal para enviar a solicitação e aguardar a resposta voltar. Quando esse método retorna, temos uma mensagem de resposta que podemos ler para descobrir qual foi a resposta do ponto de extremidade.  
  
#### <a name="closing-objects"></a>Fechando objetos  

 Para evitar vazamento de recursos, nós fechamos objetos usados nas comunicações quando não são mais necessários.  
  
 O exemplo de código a seguir mostra um cliente básico usando a fábrica de canais para enviar uma mensagem e ler a resposta.  
  
 [!code-csharp[ChannelProgrammingBasic#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/channelprogrammingbasic/cs/clientprogram.cs#2)]
 [!code-vb[ChannelProgrammingBasic#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelprogrammingbasic/vb/clientprogram.vb#2)]
