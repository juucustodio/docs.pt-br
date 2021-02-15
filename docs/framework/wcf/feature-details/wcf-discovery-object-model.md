---
description: 'Saiba mais sobre: modelo de objeto de descoberta do WCF'
title: Modelo de objeto de descoberta do WCF
ms.date: 03/30/2017
ms.assetid: 8365a152-eacd-4779-9130-bbc48fa5c5d9
ms.openlocfilehash: e0d1c569329e0f6c5d4a6cfe4271b954299efdac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732911"
---
# <a name="wcf-discovery-object-model"></a>Modelo de objeto de descoberta do WCF

A descoberta do WCF consiste em um conjunto de tipos que fornecem um modelo de programação unificado que permite que você escreva serviços que sejam detectáveis em tempo de execução e clientes que encontrem e usem esses serviços.  
  
## <a name="making-a-service-discoverable-and-finding-services"></a>Tornando um serviço detectável e encontrando serviços  

 Para tornar detectável um serviço WCF, adicione um <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> ao <xref:System.ServiceModel.Description.ServiceDescription> do host de serviço e adicione um ponto de extremidade de descoberta. Se um serviço estiver configurado para enviar mensagens de comunicado (adicionando um <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> ), o comunicado será enviado quando o host de serviço for aberto e fechado.  
  
 Um cliente que deseja escutar mensagens de anúncio de serviço hospeda um serviço de anúncio e adiciona um ou mais pontos de extremidade de comunicado. O serviço de anúncio recebe mensagens de anúncio e gera eventos de comunicado.  
  
 Um cliente usa a <xref:System.ServiceModel.Discovery.DiscoveryClient> classe para procurar os serviços disponíveis. O aplicativo cliente instancia a <xref:System.ServiceModel.Discovery.DiscoveryClient> classe, passando um ponto de extremidade de descoberta que especifica onde enviar mensagens de descoberta. O cliente chama o <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> método, que envia uma `Probe` solicitação. Serviços que escutam mensagens de descoberta recebem esta `Probe` solicitação. Se o serviço corresponder aos critérios especificados no `Probe` , ele enviará uma `ProbeMatch` mensagem de volta ao cliente.  
  
## <a name="object-model"></a>Modelo de Objeto  

 A API de descoberta do WCF define as seguintes classes:  
  
- <xref:System.ServiceModel.Discovery.AnnouncementClient>  
  
- <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
  
- <xref:System.ServiceModel.Discovery.AnnouncementService>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryClient>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryMessageSequenceGenerator>  
  
- <xref:System.ServiceModel.Discovery.ServiceDiscoveryMode>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryProxy>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryService>  
  
- <xref:System.ServiceModel.Discovery.DiscoveryVersion>  
  
- <xref:System.ServiceModel.Discovery.DynamicEndpoint>  
  
- <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>  
  
- <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>  
  
- <xref:System.ServiceModel.Discovery.FindCriteria>  
  
- <xref:System.ServiceModel.Discovery.FindRequestContext>  
  
- <xref:System.ServiceModel.Discovery.FindResponse>  
  
- <xref:System.ServiceModel.Discovery.ResolveCriteria>  
  
- <xref:System.ServiceModel.Discovery.ResolveResponse>  
  
- <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>  

- <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
  
- <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
  
## <a name="announcementclient"></a>AnnouncementClient  

 A <xref:System.ServiceModel.Discovery.AnnouncementClient> classe fornece métodos síncronos e assíncronos para enviar mensagens de anúncio. Há dois tipos de mensagens de comunicado, saudações e adeus. Uma mensagem de saudação é enviada para indicar que um serviço tornou-se disponível e uma mensagem de adeus é enviada para indicar que um serviço existente tornou-se indisponível. O desenvolvedor cria uma <xref:System.ServiceModel.Discovery.AnnouncementClient> instância, passando uma instância do <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> como um parâmetro de construtor.  
  
## <a name="announcementendpoint"></a>AnnouncementEndpoint  

 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> representa um ponto de extremidade padrão com um contrato de comunicado fixo. Ele é usado por um serviço ou cliente para enviar e receber mensagens de comunicado. Por padrão, a <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> classe é definida para usar a versão do protocolo WS_Discovery 11.  
  
## <a name="announcementservice"></a>AnnouncementService  

 <xref:System.ServiceModel.Discovery.AnnouncementService> é uma implementação fornecida pelo sistema de um serviço de anúncio que recebe e processa mensagens de anúncio. Quando uma mensagem Hello ou adeus é recebida, a <xref:System.ServiceModel.Discovery.AnnouncementService> instância chama o método virtual apropriado <xref:System.ServiceModel.Discovery.AnnouncementService.OnBeginOnlineAnnouncement%2A> ou <xref:System.ServiceModel.Discovery.AnnouncementService.OnBeginOfflineAnnouncement%2A> , que gera eventos de anúncio.  
  
## <a name="discoveryclient"></a>DiscoveryClient  

 A <xref:System.ServiceModel.Discovery.DiscoveryClient> classe é usada por um aplicativo cliente para localizar e resolver os serviços disponíveis. Ele fornece métodos síncronos e assíncronos para localizar e resolver serviços com base no especificado <xref:System.ServiceModel.Discovery.FindCriteria> e, <xref:System.ServiceModel.Discovery.ResolveCriteria> respectivamente. O desenvolvedor cria uma <xref:System.ServiceModel.Discovery.DiscoveryClient> instância do e fornece uma instância do <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> como um parâmetro de construtor.  
  
 Para encontrar um serviço, o desenvolvedor invoca o método síncrono ou assíncrono `Find` , que fornece uma <xref:System.ServiceModel.Discovery.FindCriteria> instância que contém os critérios de pesquisa a serem usados. O <xref:System.ServiceModel.Discovery.DiscoveryClient> cria uma `Probe` mensagem com os cabeçalhos apropriados e envia a solicitação de localização. Como pode haver mais de uma solicitação pendente a `Find` qualquer momento, o cliente correlaciona as respostas recebidas e valida a resposta. Em seguida, ele entrega os resultados para o chamador da `Find` operação usando <xref:System.ServiceModel.Discovery.FindResponse> .  
  
 Para resolver um serviço conhecido, o desenvolvedor invoca o método síncrono ou assíncrono `Resolve` que fornece uma instância do <xref:System.ServiceModel.Discovery.ResolveCriteria> que contém o <xref:System.ServiceModel.EndpointAddress> do serviço conhecido. O <xref:System.ServiceModel.Discovery.DiscoveryClient> cria a `Resolve` mensagem com os cabeçalhos apropriados e envia a solicitação de resolução. A resposta recebida é correlacionada às solicitações de resolução pendentes e o resultado é entregue ao chamador da `Resolve` operação usando <xref:System.ServiceModel.Discovery.ResolveResponse> .  
  
 Se um proxy de descoberta estiver presente na rede e o <xref:System.ServiceModel.Discovery.DiscoveryClient> enviar a solicitação de descoberta de uma maneira multicast, o proxy de descoberta poderá responder com a mensagem de saudação de supressão de multicast. O <xref:System.ServiceModel.Discovery.DiscoveryClient> gera o `ProxyAvailable` evento quando recebe mensagens de saudação em resposta a pendências `Find` ou `Resolve` solicitações. O `ProxyAvailable` evento contém o <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> sobre o proxy de descoberta. Cabe ao desenvolvedor usar essas informações para mudar de ad hoc para o modo gerenciado.  
  
## <a name="discoveryendpoint"></a>DiscoveryEndpoint  

 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> representa um ponto de extremidade padrão com um contrato de descoberta fixo. Ele é usado por um serviço ou cliente para enviar ou receber mensagens de descoberta. Por padrão, <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> é definido para <xref:System.ServiceModel.Discovery.ServiceDiscoveryMode.Managed?displayProperty=nameWithType> o modo de uso e a versão de WS-Discovery WSDiscovery11.  
  
## <a name="discoverymessagesequencegenerator"></a>DiscoveryMessageSequenceGenerator  

 <xref:System.ServiceModel.Discovery.DiscoveryMessageSequenceGenerator> é usado para gerar um <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence> quando o serviço está enviando mensagens de descoberta ou de anúncio.  
  
## <a name="discoveryservice"></a>DiscoveryService  

 A <xref:System.ServiceModel.Discovery.DiscoveryService> classe abstract fornece uma estrutura para receber e processar `Probe` e `Resolve` mensagens. Quando uma `Probe` mensagem é recebida, <xref:System.ServiceModel.Discovery.DiscoveryService> o cria uma instância do <xref:System.ServiceModel.Discovery.FindRequestContext> com base na mensagem de entrada e invoca o <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginFind%2A> método virtual. Quando uma `Resolve` mensagem é recebida, <xref:System.ServiceModel.Discovery.DiscoveryService> invoca o <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginResolve%2A> método virtual. Você pode herdar dessa classe para fornecer uma implementação de serviço de descoberta personalizada.  
  
## <a name="discoveryproxy"></a>DiscoveryProxy  

 A <xref:System.ServiceModel.Discovery.DiscoveryProxy> classe abstract fornece uma estrutura para receber e processar mensagens de anúncio e descoberta. Você herda dessa classe quando está implementando um proxy de descoberta personalizado. Quando uma `Probe` mensagem é recebida por multicast, a <xref:System.ServiceModel.Discovery.DiscoveryProxy> classe chama o `BeginShouldRedirectFind` método virtual para determinar se uma mensagem de supressão de multicast deve ser enviada. Se o desenvolvedor decidir não enviar uma mensagem de supressão multicast ou se a `Probe` mensagem tiver sido recebida por unicast, ela criará uma instância da <xref:System.ServiceModel.Discovery.FindRequestContext> classe com base na mensagem de entrada e invocará o `OnBeginFind` método virtual. Quando uma `Resolve` mensagem é recebida por multicast, a <xref:System.ServiceModel.Discovery.DiscoveryProxy> classe chama o `ShouldRedirectResolve` método virtual para determinar se uma mensagem de supressão de multicast deve ser enviada. Se o desenvolvedor decidir não enviar uma mensagem de supressão multicast ou se a `Resolve` mensagem tiver sido recebida por unicast, ela criará uma instância da <xref:System.ServiceModel.Discovery.ResolveCriteria> classe com base na mensagem de entrada e invocará o `OnBeginResolve` método virtual. Quando uma mensagem Hello ou adeus é recebida, <xref:System.ServiceModel.Discovery.DiscoveryProxy> o chama o método virtual apropriado ( `OnBeginOnlineAnnouncement` ou `OnBeingOfflineAnnouncement` ), que gera eventos de comunicado.  
  
## <a name="discoveryversion"></a>DiscoveryVersion  

 A <xref:System.ServiceModel.Discovery.DiscoveryVersion> classe representa a versão do protocolo de descoberta a ser usada.  
  
## <a name="endpointdiscoverybehavior"></a>EndpointDiscoveryBehavior  

 A <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> classe é usada para controlar a capacidade de descoberta de um ponto de extremidade, especificar as extensões, os nomes de tipo de contrato adicionais. e os escopos associados a esse ponto de extremidade. Esse comportamento é adicionado a um ponto de extremidade de aplicativo para configurar seu <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> . Quando <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> é adicionado ao host de serviço, todos os pontos de extremidade do aplicativo hospedados pelo host de serviço, por padrão, se tornam detectáveis. O desenvolvedor pode desativar a descoberta para um ponto de extremidade específico definindo a <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior.Enabled%2A> propriedade como `false` .  
  
## <a name="endpointdiscoverymetadata"></a>EndpointDiscoveryMetadata  

 A <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> classe fornece uma representação independente de versão de um ponto de extremidade publicado pelo serviço. Ele contém endereços de ponto de extremidade, URIs de escuta, nomes de tipo de contrato, escopos, versão de metadados e extensões especificados pelo desenvolvedor de serviço. O <xref:System.ServiceModel.Discovery.FindCriteria> enviado pelo cliente durante uma `Probe` operação é correspondido em relação ao <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> . Se os critérios corresponderem, o <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> será retornado ao cliente. O endereço do ponto de extremidade no <xref:System.ServiceModel.Discovery.ResolveCriteria> é correspondido em relação ao endereço do ponto de extremidade de <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> . Se os critérios corresponderem, o <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> será retornado ao cliente.  
  
## <a name="findcriteria"></a>FindCriteria  

 A <xref:System.ServiceModel.Discovery.FindCriteria> classe é uma classe independente de versão usada para especificar os critérios usados ao localizar um serviço. Ele dá suporte completo aos critérios definidos pelo WS-Discovery para serviços correspondentes. Ele também tem extensões que os desenvolvedores podem usar para especificar valores personalizados que podem ser usados durante o processo de correspondência. O desenvolvedor pode fornecer os critérios de encerramento para a `Find` operação especificando o <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> , que especifica o número total de serviços que o desenvolvedor está procurando ou que especifica o <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> , que é o valor que especifica por quanto tempo o cliente aguarda as respostas.  
  
## <a name="findrequestcontext"></a>FindRequestContext  

 A <xref:System.ServiceModel.Discovery.FindRequestContext> classe é instanciada pelo serviço de descoberta com base na `Probe` mensagem recebida quando um cliente inicia uma `Find` operação. Ele contém uma instância do <xref:System.ServiceModel.Discovery.FindCriteria> que foi especificada pelo cliente.  
  
## <a name="findresponse"></a>FindResponse  

 A <xref:System.ServiceModel.Discovery.FindResponse> classe é retornada ao chamador de <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> com as respostas da `Find` operação. Ele também está presente no <xref:System.ServiceModel.Discovery.FindCompletedEventArgs> . Ele contém uma coleção de <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> , que é a coleção de pontos de extremidade descobertos e um dicionário de <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> e <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence> .  
  
## <a name="resolvecriteria"></a>ResolveCriteria  

 A <xref:System.ServiceModel.Discovery.ResolveCriteria> classe é uma classe independente de versão usada para especificar os critérios usados ao resolver um serviço já conhecido. Ele contém o endereço do ponto de extremidade do serviço conhecido. O desenvolvedor pode fornecer os critérios de encerramento para a operação de resolução especificando o <xref:System.ServiceModel.Discovery.ResolveCriteria.Duration%2A> , que especifica por quanto tempo o cliente aguarda as respostas.  
  
## <a name="resolveresponse"></a>ResolveResponse  

 O <xref:System.ServiceModel.Discovery.ResolveResponse> é retornado para o chamador do <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> método com a resposta da `Resolve` operação. Ele também está presente no <xref:System.ServiceModel.Discovery.ResolveCompletedEventArgs> . Ele contém uma instância do <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> , que são os pontos de extremidade descobertos e uma instância do <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence> .  
  
## <a name="servicediscoverybehavior"></a>ServiceDiscoveryBehavior  

 A <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> classe permite que o desenvolvedor adicione o recurso de descoberta a um serviço. Você adiciona esse comportamento ao <xref:System.ServiceModel.ServiceHost> . A <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> classe itera sobre os pontos de extremidade do aplicativo adicionados ao host de serviço e cria uma coleção de <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> pontos de extremidade detectáveis. Todos os pontos de extremidade são detectáveis por padrão. A capacidade de descoberta de um ponto de extremidade específico pode ser controlada adicionando o <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> ao ponto de extremidade específico. Se os pontos de extremidade do comunicado forem adicionados <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> , o anúncio de todos os pontos de extremidade detectáveis será enviado em cada um dos pontos de extremidade do comunicado quando o host de serviço for aberto ou fechado.  
  
## <a name="udpannouncementendpoint"></a>UdpAnnouncementEndpoint  

 A <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> classe é um ponto de extremidade de anúncio padrão pré-configurado para o anúncio em uma associação de multicast UDP. Por padrão, <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> é definido para usar a versão WS_Discovery do WSApril2005.  
  
## <a name="udpdiscoveryendpoint"></a>UdpDiscoveryEndpoint  

 A <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> classe é um ponto de extremidade de descoberta padrão pré-configurado para descoberta em uma associação de multicast UDP. Por padrão, <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> é definido para usar a versão e o modo WSDiscovery11 WS-Discovery <xref:System.ServiceModel.Discovery.ServiceDiscoveryMode.Adhoc?displayProperty=nameWithType> .
