---
description: 'Saiba mais sobre: escolhendo um padrão de troca de mensagens'
title: Escolhendo um padrão de troca de mensagens
ms.date: 03/30/2017
ms.assetid: 0f502ca1-6a8e-4607-ba15-59198c0e6146
ms.openlocfilehash: c452a65e4d4108123deaab93be9bd825127eba70
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685849"
---
# <a name="choosing-a-message-exchange-pattern"></a>Escolhendo um padrão de troca de mensagens

A primeira etapa na gravação de um transporte personalizado é decidir quais *padrões de troca de mensagens* (ou MEPS) são necessários para o canal que você está desenvolvendo. Este tópico descreve as opções disponíveis e discute os vários requisitos. Esta é a primeira tarefa na lista de tarefas de desenvolvimento de canal descrita em [desenvolvimento de canais](developing-channels.md).  
  
## <a name="six-message-exchange-patterns"></a>Seis padrões de troca de mensagens  

 Há três MEPs de escolha:  
  
- Datagrama ( <xref:System.ServiceModel.Channels.IInputChannel> e <xref:System.ServiceModel.Channels.IOutputChannel> )  
  
     Ao usar um dataMEP de datagrama, um cliente envia uma mensagem usando um *incêndio e esquece* o Exchange. Um incêndio e esquecido o Exchange é um que requer a confirmação fora de banda da entrega bem-sucedida. A mensagem pode ser perdida em trânsito e nunca alcançar o serviço. Se a operação de envio for concluída com êxito na extremidade do cliente, ela não garante que o ponto de extremidade remoto tenha recebido a mensagem. O datagrama é um bloco de construção fundamental para mensagens, pois você pode criar seus próprios protocolos sobre ele, incluindo protocolos confiáveis e protocolos seguros. Canais de datagrama de cliente implementam a <xref:System.ServiceModel.Channels.IOutputChannel> interface e os canais de datagrama de serviço implementam a <xref:System.ServiceModel.Channels.IInputChannel> interface.  
  
- Request-Response ( <xref:System.ServiceModel.Channels.IRequestChannel> e <xref:System.ServiceModel.Channels.IReplyChannel> )  
  
     Neste MEP, uma mensagem é enviada e uma resposta é recebida. O padrão consiste em pares de solicitação-resposta. Exemplos de chamadas de solicitação-resposta são RPC (chamadas de procedimento remoto) e solicitações GET de navegador. Esse padrão também é conhecido como Half-duplex. Neste MEP, os canais de cliente implementam o <xref:System.ServiceModel.Channels.IRequestChannel> e os canais de serviço implementam <xref:System.ServiceModel.Channels.IReplyChannel> .  
  
- Duplex ( <xref:System.ServiceModel.Channels.IDuplexChannel> )  
  
     O MEP duplex permite que um número arbitrário de mensagens seja enviado por um cliente e recebido em qualquer ordem. O duplex MEP é como uma conversa telefônica, onde cada palavra que está sendo falada é uma mensagem. Como ambos os lados podem enviar e receber neste MEP, a interface implementada pelos canais de cliente e de serviço é <xref:System.ServiceModel.Channels.IDuplexChannel> .  
  
 ![Escolhendo um padrão de troca de mensagens](./media/wcfc-basicthreemepsc.gif "wcfc_BasicThreeMEPsc")  
Os três padrões básicos de troca de mensagens. De cima para baixo: datagrama, solicitação-resposta e duplex.  
  
 Cada um desses MEPs também pode dar suporte a *sessões*. Uma sessão (e implementação do <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=nameWithType> tipo <xref:System.ServiceModel.Channels.ISession?displayProperty=nameWithType> ) correlaciona todas as mensagens enviadas e recebidas em um canal. O padrão de solicitação-resposta é uma sessão autônoma de duas mensagens, pois a solicitação e a resposta são correlacionadas. Por outro lado, o padrão de solicitação-resposta que dá suporte a sessões implica que todos os pares de solicitação/resposta nesse canal estão correlacionados entre si. Isso lhe dá um total de seis MEPs para escolher:  
  
- Datagrama  
  
- Solicitação-resposta  
  
- Duplex  
  
- Datagrama com sessões  
  
- Solicitação-resposta com sessões  
  
- Duplex com sessões  
  
> [!NOTE]
> Para o transporte UDP, o único MEP com suporte é datagrama, pois o UDP é inerentemente a um protocolo Fire e esqueça.  
  
## <a name="sessions-and-sessionful-channels"></a>Sessões e canais de sessão  

 No mundo de rede, há protocolos orientados a conexões (por exemplo, TCP) e protocolos sem conexão (por exemplo, UDP). O WCF usa a sessão de termo para significar uma abstração lógica como uma conexão. Os protocolos WCF de sessão são semelhantes aos protocolos de rede orientados a conexões e os protocolos WCF sem sessão são semelhantes aos protocolos de rede com menos conexão.  
  
 No modelo de objeto do canal, cada sessão lógica é manifestada como uma instância de um canal de sessão. Portanto, todas as novas sessões criadas pelo cliente e aceitas no serviço correspondem a um novo canal de sessão em cada lado. O diagrama a seguir mostra, na parte superior, a estrutura de canais de sessão e, na parte inferior, a estrutura de canais de sessão.  
  
 ![Escolhendo um padrão de troca de mensagens](./media/wcfc-sessionandsessionlesschannelsc.gif "wcfc_SessionAndSessionlessChannelsc")  
  
 Um cliente cria um novo canal de sessão e envia uma mensagem. No lado do serviço, o ouvinte do canal recebe essa mensagem e detecta que ela pertence a uma nova sessão, de modo que cria um novo canal de sessão e a passa para o aplicativo (em resposta ao aplicativo que chama AcceptChannel no ouvinte do canal). O aplicativo recebe essa mensagem e todas as mensagens subsequentes enviadas na mesma sessão por meio do mesmo canal de sessão.  
  
 Outro cliente (ou o mesmo cliente) cria uma nova sessão e envia uma mensagem. O ouvinte de canal detecta que essa mensagem está em uma nova sessão e cria um novo canal de sessão e o processo se repete.  
  
 Sem sessões, não há nenhuma correlação entre canais e sessões. Portanto, um ouvinte de canal cria apenas um canal pelo qual todas as mensagens recebidas são entregues ao aplicativo. Também não há nenhuma solicitação de mensagem porque não há nenhuma sessão dentro da qual manter a ordem da mensagem. A parte superior do gráfico anterior ilustra uma troca de mensagens por sessão.  
  
## <a name="starting-and-terminating-sessions"></a>Iniciando e terminando sessões  

 As sessões são iniciadas no cliente simplesmente criando um novo canal de sessão. Eles são iniciados no serviço quando o serviço recebe uma mensagem que foi enviada em uma nova sessão. Da mesma forma, as sessões são encerradas fechando ou anulando um canal de sessão.  
  
 A exceção é <xref:System.ServiceModel.Channels.IDuplexSessionChannel> que é usada para enviar e receber mensagens em um padrão de comunicação duplex e de sessão. É possível que um lado queira parar de enviar mensagens, mas continuar recebendo mensagens, portanto, ao usar <xref:System.ServiceModel.Channels.IDuplexSessionChannel> há um mecanismo que permite fechar a sessão de saída, indicando que você não enviará mais mensagens, mas manterá a sessão de entrada aberta, permitindo que você continue a receber mensagens.  
  
 Em geral, as sessões são fechadas no lado de saída e não no lado de entrada. Ou seja, os canais de saída de sessão podem ser fechados, encerrando assim a sessão. Fechar um canal de saída de sessão faz com que o canal de entrada da sessão correspondente retorne nulo para a chamada do aplicativo <xref:System.ServiceModel.Channels.IInputChannel.Receive%2A?displayProperty=nameWithType> no <xref:System.ServiceModel.Channels.IDuplexSessionChannel> .  
  
 No entanto, os canais de entrada de sessão não devem ser fechados, a menos que <xref:System.ServiceModel.Channels.IInputChannel.Receive%2A?displayProperty=nameWithType> em <xref:System.ServiceModel.Channels.IDuplexSessionChannel> retorna NULL, indicando que a sessão já está fechada. Se <xref:System.ServiceModel.Channels.IInputChannel.Receive%2A?displayProperty=nameWithType> em <xref:System.ServiceModel.Channels.IDuplexSessionChannel> não tiver retornado NULL, o fechamento de um canal de entrada de sessão poderá gerar uma exceção, pois poderá receber mensagens inesperadas durante o fechamento. Se um receptor quiser encerrar uma sessão antes do remetente, ele deverá chamar <xref:System.ServiceModel.ICommunicationObject.Abort%2A> no canal de entrada, que finalizará abruptamente a sessão.  
  
## <a name="writing-sessionful-channels"></a>Gravando canais de sessão  

 Como um autor de canal de sessão, há algumas coisas que seu canal deve fazer para fornecer sessões. No lado do envio, seu canal precisa:  
  
- Para cada novo canal, crie uma nova sessão e associe-a a uma nova ID de sessão, que é uma cadeia de caracteres exclusiva. Ou obtenha uma nova sessão do canal de sessão abaixo da pilha.  
  
- Para cada mensagem enviada usando esse canal, se o canal tiver criado a sessão (em vez de obtê-la da camada abaixo), você precisará associar a mensagem à sessão. Para canais de protocolo, isso normalmente é feito adicionando um cabeçalho SOAP. Para canais de transporte, isso normalmente é feito criando uma nova conexão de transporte ou adicionando informações de sessão ao protocolo de enquadramento.  
  
- Para cada mensagem enviada usando esse canal, você precisa fornecer as garantias de entrega mencionadas acima. Se você estiver contando com o canal abaixo de fornecer a sessão, esse canal também fornecerá as garantias de entrega. Se você estiver fornecendo a sessão por conta própria, precisará implementar essas garantias como parte do seu protocolo. Em geral, se você estiver escrevendo um canal de protocolo que assume o WCF em ambos os lados, poderá exigir o transporte TCP ou o canal de mensagens confiáveis e confiar em qualquer um para fornecer uma sessão.  
  
- Quando o <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=nameWithType> for chamado em seu canal, execute o trabalho necessário para fechar a sessão usando o tempo limite especificado ou o padrão. Isso pode ser tão simples quanto chamar <xref:System.ServiceModel.ICommunicationObject.Close%2A> no canal abaixo de você (se você acabou de obter a sessão a partir dele) ou enviar uma mensagem SOAP especial ou fechar uma conexão de transporte.  
  
- Quando <xref:System.ServiceModel.ICommunicationObject.Abort%2A> é chamado em seu canal, encerre a sessão abruptamente sem executar e/s. Isso pode significar não fazer nada ou pode envolver a anulação de uma conexão de rede ou de algum outro recurso.  
  
 No lado do recebimento, seu canal precisa:  
  
- Para cada mensagem de entrada, o ouvinte do canal deve detectar a sessão à qual pertence. Se esta for a primeira mensagem na sessão, o ouvinte do canal deverá criar um novo canal e retorná-lo da chamada para <xref:System.ServiceModel.Channels.IChannelListener%601.AcceptChannel%2A?displayProperty=nameWithType> . Caso contrário, o ouvinte do canal deve encontrar o canal existente que corresponde à sessão e entregar a mensagem por meio desse canal.  
  
- Se o canal estiver fornecendo a sessão (juntamente com as garantias de entrega necessárias), o lado de recebimento poderá ser necessário para executar algumas ações, como reordenar mensagens ou enviar confirmações.  
  
- Quando o <xref:System.ServiceModel.ICommunicationObject.Close%2A> for chamado em seu canal, execute o trabalho necessário para fechar a sessão com o tempo limite especificado ou o padrão. Isso pode resultar em exceções se o canal receber uma mensagem enquanto aguarda o tempo limite de fechamento expirar. Isso ocorre porque o canal estará no estado de fechamento quando receber uma mensagem para que ele seja gerado.  
  
- Quando <xref:System.ServiceModel.ICommunicationObject.Abort%2A> é chamado em seu canal, encerre a sessão abruptamente sem executar e/s. Novamente, isso pode significar não fazer nada ou pode envolver a anulação de uma conexão de rede ou de algum outro recurso.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral de modelo de canal](channel-model-overview.md)
