---
description: 'Saiba mais sobre: projetando e implementando serviços'
title: Serviços de implantação e projeção
ms.date: 03/30/2017
helpviewer_keywords:
- defining service contracts [WCF]
ms.assetid: 036fae20-7c55-4002-b71d-ac4466e167a3
ms.openlocfilehash: fde63fb6d1256b3c9e1fdd69932e378de95d508b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646069"
---
# <a name="designing-and-implementing-services"></a>Serviços de implantação e projeção

Esta seção mostra como definir e implementar contratos do WCF. Um contrato de serviço especifica o que um ponto de extremidade se comunica com o mundo exterior. Em um nível mais concreto, trata-se de uma declaração sobre um conjunto de mensagens específicas organizadas em padrões de troca de mensagens básicos (MEPs), como solicitação/resposta, unidirecional e duplex. Se um contrato de serviço for um conjunto de trocas de mensagens logicamente relacionado, uma operação de serviço será uma única troca de mensagens. Por exemplo, uma `Hello` operação deve, obviamente, aceitar uma mensagem (para que o chamador possa anunciar a saudação) e pode ou não retornar uma mensagem (dependendo da cortesia da operação).  
  
 Para obter mais informações sobre contratos e outros conceitos de Windows Communication Foundation de núcleo (WCF), consulte [conceitos fundamentais de Windows Communication Foundation](fundamental-concepts.md). Este tópico se concentra na compreensão dos contratos de serviço. Para obter mais informações sobre como criar clientes que usam contratos de serviço para se conectar a serviços, consulte [visão geral do cliente WCF](wcf-client-overview.md).  
  
## <a name="overview"></a>Visão geral  

 Este tópico fornece uma orientação conceitual de alto nível para projetar e implementar serviços WCF. Os subtópicos fornecem informações mais detalhadas sobre as especificidades de design e implementação. Antes de projetar e implementar seu aplicativo WCF, é recomendável que você:  
  
- Entenda o que é um contrato de serviço, como ele funciona e como criar um.  
  
- Entenda que os contratos atendem aos requisitos mínimos que a configuração de tempo de execução ou o ambiente de hospedagem pode não dar suporte.  
  
## <a name="service-contracts"></a>Contratos de serviço  

 Um contrato de serviço especifica o seguinte:  
  
- As operações que um contrato expõe.  
  
- A assinatura das operações em termos de mensagens trocadas.  
  
- Os tipos de dados dessas mensagens.  
  
- O local das operações.  
  
- Os protocolos específicos e os formatos de serialização usados para dar suporte à comunicação bem-sucedida com o serviço.  
  
 Por exemplo, um contrato de ordem de compra pode ter uma `CreateOrder` operação que aceita uma entrada de tipos de informações de pedidos e retorna informações de êxito ou falha, incluindo um identificador de pedido. Ele também pode ter uma `GetOrderStatus` operação que aceita um identificador de pedido e retorna informações de status do pedido. Um contrato de serviço dessa classificação especificaria:  
  
1. O contrato de ordem de compra consistiu `CreateOrder` em `GetOrderStatus` operações e.  
  
2. Se as operações especificaram mensagens de entrada e mensagens de saída.  
  
3. Os dados que essas mensagens podem transportar.  
  
4. Instruções categóricas sobre a infraestrutura de comunicação necessária para processar as mensagens com êxito. Por exemplo, esses detalhes incluem se e quais formas de segurança são necessárias para estabelecer uma comunicação bem-sucedida.  
  
 Para transmitir esse tipo de informação a outros aplicativos em várias plataformas (incluindo plataformas não Microsoft), os contratos de serviço XML são publicamente expressos em formatos XML padrão, como WSDL ( [Web Services Description Language](https://www.w3.org/TR/2001/NOTE-wsdl-20010315) ) e XSD ( [XML Schema](https://www.w3.org/XML/Schema) ), entre outros. Os desenvolvedores de várias plataformas podem usar essas informações de contrato público para criar aplicativos que podem se comunicar com o serviço, ambos porque entendem o idioma da especificação e porque esses idiomas são projetados para permitir a interoperação descrevendo os formulários públicos, os formatos e os protocolos aos quais o serviço dá suporte. Para obter mais informações sobre como o WCF lida com esse tipo de informação, consulte [metadados](./feature-details/metadata.md).  
  
 Os contratos podem ser expressos de várias maneiras e, embora WSDL e XSD sejam excelentes linguagens para descrever os serviços de forma acessível, eles são as linguagens difíceis de usar diretamente e são apenas descrições de um serviço, não das implementações de contrato de serviço. Portanto, os aplicativos WCF usam atributos, interfaces e classes gerenciados para definir a estrutura de um serviço e para implementá-lo.  
  
 O contrato resultante definido em tipos gerenciados pode ser *exportado* como metadados — WSDL e XSD — quando necessário para os clientes ou outros implementadores de serviço. O resultado é um modelo de programação simples que pode ser descrito (usando metadados públicos) para qualquer aplicativo cliente. Os detalhes das mensagens SOAP subjacentes, o transporte e as informações relacionadas à segurança e assim por diante podem ser deixados para o WCF, que executa as conversões necessárias de e para o sistema de tipo de contrato de serviço para o sistema de tipos XML automaticamente.  
  
 Para obter mais informações sobre como criar contratos, consulte [projetando contratos de serviço](designing-service-contracts.md). Para obter mais informações sobre como implementar contratos, consulte [implementando contratos de serviço](implementing-service-contracts.md).  
  
### <a name="messages-up-front-and-center"></a>Mensagens de frente e de centro  

 O uso de interfaces, classes e métodos gerenciados para modelar as operações de serviço é simples quando você é usado para assinaturas de método de estilo RPC (chamada de procedimento remoto), em que a passagem de parâmetros para um método e o recebimento de valores de retorno é a forma normal de solicitar funcionalidade de um objeto ou outro tipo de código. Por exemplo, os programadores que usam linguagens gerenciadas como Visual Basic e C++ COM podem aplicar seu conhecimento da abordagem no estilo RPC (seja usando objetos ou interfaces) à criação de contratos de serviço do WCF sem enfrentar os problemas inerentes em sistemas de objetos distribuídos no estilo RPC. A orientação do serviço fornece os benefícios da programação menos rígida e orientada a mensagens, mantendo a facilidade e a familiaridade da experiência de programação de RPC.  
  
 Muitos programadores são mais confortáveis com interfaces de programação de aplicativo orientadas a mensagens, como filas de mensagens como o Microsoft MSMQ, os <xref:System.Messaging> namespaces no .NET Framework ou o envio de XML não estruturado em solicitações HTTP, para citar alguns. Para obter mais informações sobre programação no nível da mensagem, consulte [usando contratos de mensagem](./feature-details/using-message-contracts.md), [programação de Channel-Level de serviço](./extending/service-channel-level-programming.md)e [interoperabilidade com aplicativos Pox](./feature-details/interoperability-with-pox-applications.md).  
  
### <a name="understanding-the-hierarchy-of-requirements"></a>Noções básicas sobre a hierarquia de requisitos  

 Um contrato de serviço agrupa as operações; Especifica o padrão de troca de mensagens, os tipos de mensagem e os tipos de dados que essas mensagens executam; e indica categorias de comportamento de tempo de execução que uma implementação deve ter para dar suporte ao contrato (por exemplo, pode exigir que as mensagens sejam criptografadas e assinadas). O próprio contrato de serviço não especifica precisamente como esses requisitos são atendidos, apenas que eles devem ser. O tipo de criptografia ou a maneira pela qual uma mensagem é assinada é a implementação e a configuração de um serviço em conformidade.  
  
 Observe a maneira como o contrato requer determinadas coisas da implementação do contrato de serviço e a configuração de tempo de execução para adicionar o comportamento. O conjunto de requisitos que devem ser atendidos para expor um serviço para uso se baseia no conjunto de requisitos anterior. Se um contrato fizer requisitos da implementação, uma implementação poderá exigir ainda mais a configuração e as associações que permitem a execução do serviço. Por fim, o aplicativo host também deve oferecer suporte a todos os requisitos que a configuração de serviço e as associações adicionam.  
  
 Esse processo de requisito aditivo é importante para ter em mente ao projetar, implementar, configurar e hospedar um aplicativo de serviço de Windows Communication Foundation (WCF). Por exemplo, o contrato pode especificar que ele precisa oferecer suporte a uma sessão. Nesse caso, você deve configurar a associação para dar suporte a esse requisito contratual ou a implementação do serviço não funcionará. Ou se o serviço exigir autenticação integrada do Windows e estiver hospedado no Serviços de Informações da Internet (IIS), o aplicativo Web no qual o serviço reside deve ter a autenticação integrada do Windows ativada e o suporte anônimo desativado. Para obter mais informações sobre os recursos e o impacto dos diferentes tipos de aplicativo de host de serviço, consulte [serviços de hospedagem](hosting-services.md).  
  
## <a name="see-also"></a>Consulte também

- [Criando contratos de serviço](designing-service-contracts.md)
- [Implementando contratos de serviço](implementing-service-contracts.md)
