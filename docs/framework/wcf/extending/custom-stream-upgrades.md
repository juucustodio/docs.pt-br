---
description: 'Saiba mais sobre: atualizações de fluxo personalizadas'
title: Atualizações de fluxo personalizadas
ms.date: 03/30/2017
ms.assetid: e3da85c8-57f3-4e32-a4cb-50123f30fea6
ms.openlocfilehash: fe52b99de382d5a5d5b41a0bff2c4a9a7698f6f5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735238"
---
# <a name="custom-stream-upgrades"></a>Atualizações de fluxo personalizadas

Transportes orientados a fluxo, como TCP e pipes nomeados, operam em um fluxo contínuo de bytes entre o cliente e o servidor. Esse fluxo é percebido por um  <xref:System.IO.Stream> objeto. Em uma atualização de fluxo, o cliente deseja adicionar uma camada de protocolo opcional à pilha de canais e faz com que a outra extremidade do canal de comunicação faça isso. A atualização do fluxo consiste em substituir o <xref:System.IO.Stream> objeto original por um atualizado.  
  
 Por exemplo, você pode criar um fluxo de compactação diretamente na parte superior do fluxo de transporte. Nesse caso, o transporte original <xref:System.IO.Stream> é substituído por um que encapsula a compactação <xref:System.IO.Stream> em todo o original.  
  
 Você pode aplicar várias atualizações de fluxo, cada uma encapsulando a anterior.  
  
## <a name="how-stream-upgrades-work"></a>Como as atualizações de fluxo funcionam  

 Há quatro componentes para o processo de atualização de fluxo.  
  
1. Um *iniciador* de fluxo de atualização inicia o processo: em tempo de execução, ele pode iniciar uma solicitação para a outra extremidade de sua conexão para atualizar a camada de transporte de canal.  
  
2. Um *aceitor* de fluxo de atualização executa a atualização: em tempo de execução, ele recebe a solicitação de atualização do outro computador e, se possível, aceita a atualização.  
  
3. Um *provedor* de atualização cria o *iniciador* no cliente e o *aceitor* no servidor.  
  
4. Um elemento de *Associação* de atualização de fluxo é adicionado às associações no serviço e no cliente e cria o provedor em tempo de execução.  
  
 Observe que, no caso de várias atualizações, o iniciador e o Aceitor encapsulam máquinas de estado para impor quais transições de atualização são válidas para cada inicialização.  
  
## <a name="how-to-implement-a-stream-upgrade"></a>Como implementar uma atualização de fluxo  

 O Windows Communication Foundation (WCF) fornece quatro `abstract` classes que podem ser implementadas:  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeInitiator?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeProvider?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement?displayProperty=nameWithType>  
  
 Para implementar uma atualização de fluxo personalizada, faça o seguinte. Esse procedimento implementa um processo de atualização de fluxo mínimo nos computadores cliente e servidor.  
  
1. Crie uma classe que implementa <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>.  
  
    1. Substitua o <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.InitiateUpgrade%2A> método a ser retirado no fluxo a ser atualizado e retorne o fluxo atualizado. Esse método funciona de forma síncrona; Há métodos análogos para iniciar a atualização de forma assíncrona.  
  
    2. Substitua o <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> método para verificar se há atualizações adicionais.  
  
2. Crie uma classe que implementa <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>.  
  
    1. Substitua o <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.AcceptUpgrade%2A> método a ser retirado no fluxo a ser atualizado e retorne o fluxo atualizado. Esse método funciona de forma síncrona; Há métodos análogos para aceitar a atualização de forma assíncrona.  
  
    2. Substitua o <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> método para determinar se a atualização solicitada tem suporte por esse aceitador de atualização neste momento no processo de atualização.  
  
3. Crie uma classe que o implementa <xref:System.ServiceModel.Channels.StreamUpgradeProvider> . Substitua os <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeAcceptor%2A> métodos e <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeInitiator%2A> para retornar as instâncias do aceitador e do iniciador definidos nas etapas 2 e 1.  
  
4. Crie uma classe que implementa <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>.  
  
    1. Substitua o <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildClientStreamUpgradeProvider%2A> método no cliente e o <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildServerStreamUpgradeProvider%2A> método no serviço.  
  
    2. Substitua o <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> método no cliente e o <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> método no serviço ao qual adicionar o elemento de associação de atualização <xref:System.ServiceModel.Channels.BindingContext.BindingParameters%2A> .  
  
5. Adicione o novo elemento de associação de atualização de fluxo a associações nos computadores servidor e cliente.  
  
## <a name="security-upgrades"></a>Atualizações de segurança  

 A adição de uma atualização de segurança é uma versão especializada do processo geral de atualização de fluxo.  
  
 O WCF já fornece dois elementos de ligação para atualizar a segurança do fluxo. A configuração da segurança em nível de transporte é encapsulada pelo <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement> e o <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement> que pode ser configurado e adicionado a uma associação personalizada. Esses elementos de ligação estendem a <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> classe que cria os provedores de atualização de fluxo do cliente e do servidor. Esses elementos de ligação têm métodos que criam as classes especializadas do provedor de atualização de fluxo de segurança, que não são `public` , portanto, para esses dois casos, tudo o que você precisa fazer é adicionar o elemento de associação à associação.  
  
 Para cenários de segurança não atendidos pelos dois elementos de ligação acima, três classes relacionadas à segurança `abstract` são derivadas das classes de iniciador, aceiter e provedor acima:  
  
1. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator?displayProperty=nameWithType>  
  
2. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor?displayProperty=nameWithType>  
  
3. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider?displayProperty=nameWithType>  
  
 O processo de implementação de uma atualização de fluxo de segurança é o mesmo que antes, com a diferença que você deriva dessas três classes. Substitua as propriedades adicionais nessas classes para fornecer informações de segurança para o tempo de execução.  
  
## <a name="multiple-upgrades"></a>Várias atualizações  

 Para criar solicitações de atualização adicionais, repita o processo acima: criar extensões <xref:System.ServiceModel.Channels.StreamUpgradeProvider> e elementos de associação adicionais. Adicione os elementos de associação à associação. Os elementos de associação adicionais são processados sequencialmente, começando com o primeiro elemento de associação adicionado à associação. Em <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> e <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> cada provedor de atualização pode determinar como fazer a camada em qualquer parâmetro de associação de atualização pré-existente. Em seguida, ele deve substituir o parâmetro de associação de atualização existente por um novo parâmetro de associação de atualização composta.  
  
 Como alternativa, um provedor de atualização pode dar suporte a várias atualizações. Por exemplo, talvez você queira implementar um provedor de atualização de fluxo personalizado que dê suporte à segurança e à compactação. Execute as seguintes etapas:  
  
1. Subclasse <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider> para gravar a classe de provedor que cria o iniciador e o aceiter.  
  
2. Subclasse a que <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator> se certifique de substituir o <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> método para retornar os tipos de conteúdo para o fluxo de compactação e o fluxo seguro na ordem.  
  
3. Subclasse o <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor> que entende os tipos de conteúdo personalizados em seu <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> método.  
  
4. O fluxo será atualizado após cada chamada para <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> e <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> .  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator>
- <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor>
- <xref:System.ServiceModel.Channels.StreamUpgradeProvider>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider>
- <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>
