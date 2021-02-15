---
description: 'Saiba mais sobre: associações e elementos de associação'
title: Associações e elementos de associações
ms.date: 03/30/2017
helpviewer_keywords:
- binding elements [WCF]
ms.assetid: 765ff77b-7682-4ea3-90eb-e4d751e37379
ms.openlocfilehash: 0d43a676bf5b4a166a34a2d623e0f80cc9df66f0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756715"
---
# <a name="bindings-and-binding-elements"></a>Associações e elementos de associações

Associações são coleções de elementos de configuração especiais, chamadas de *elementos de associação*, que são avaliadas pelo tempo de execução do serviço sempre que um cliente ou ponto de extremidade de serviço está sendo construído. O tipo e a ordem dos elementos de associação dentro de uma associação determinam a ordem de seleção e de empilhamento do protocolo e dos canais de transporte na pilha de canais de um ponto de extremidade.  
  
 Associações, especialmente as associações fornecidas pelo sistema, geralmente também têm várias propriedades de configuração que refletem as propriedades mais modificadas dos elementos de ligação encapsulados.  
  
 Uma associação deve conter exatamente um elemento de associação de transporte. Cada elemento de associação de transporte implica um elemento de associação de codificação de mensagem padrão, que pode ser substituído adicionando no máximo um elemento de associação de codificação de mensagem à associação. Além dos elementos de associação de codificador e de transporte, a associação pode conter qualquer número de elementos de ligação de protocolo que, juntos, implementam a funcionalidade necessária para atender e enviar uma mensagem SOAP de um ponto de extremidade para outro. Para obter detalhes, consulte [usando associações para configurar serviços e clientes](../using-bindings-to-configure-services-and-clients.md).  
  
## <a name="extending-bindings-and-binding-elements"></a>Estendendo associações e elementos de associação  

 O Windows Communication Foundation (WCF) inclui associações fornecidas pelo sistema que abrangem uma ampla gama de cenários. (Para obter mais informações, consulte [associações fornecidas pelo sistema](../system-provided-bindings.md).) No entanto, pode haver ocasiões em que você precisa criar e usar uma associação que não está incluída no WCF. Os cenários a seguir exigem a criação de uma nova associação.  
  
- Para usar um novo elemento de associação (como um novo elemento de transporte, codificação ou associação de protocolo), você deve criar uma nova associação que inclua esse elemento de associação. Por exemplo, se você adicionou um personalizado `UdpTransportBindingElement` para transporte UDP, precisaria criar uma nova associação para fazer uso dele. Para obter informações sobre como executar esse comportamento usando o <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> tipo, consulte [associações personalizadas](custom-bindings.md).  
  
- Para configurar elementos de associação existentes de uma maneira que as associações fornecidas pelo sistema não sejam expostas em propriedades públicas. Por exemplo, você deve criar uma nova associação para alterar a ordem na qual as operações de assinatura e criptografia são executadas. Para obter informações sobre como executar esse comportamento, consulte [como: personalizar uma associação de System-Provided](how-to-customize-a-system-provided-binding.md).  
  
- Para estabelecer associações padrão corporativas que expõem apenas opções de configuração específicas. Por exemplo, para criar para sua empresa uma variante do <xref:System.ServiceModel.WSHttpBinding> para sua empresa na qual a segurança não pode ser desabilitada, crie uma nova associação que se comporta como a <xref:System.ServiceModel.WSHttpBinding> , mas com segurança AlwaysOn. Para obter detalhes, consulte [Criando associações de User-Defined](creating-user-defined-bindings.md).  
  
- Para executar algumas personalizações de metadados, normalmente, mas não necessariamente para configurar ou usar algum elemento de ligação personalizado. Para obter mais informações sobre como fornecer suporte de metadados a associações e elementos de associação, consulte [suporte de configuração e metadados](configuration-and-metadata-support.md).  

## <a name="channels-bindings-and-binding-elements"></a>Canais, associações e elementos de associação  

 Associações e elementos de associação são a conexão entre o modelo de programação de aplicativo, que inclui os atributos e comportamentos, e o modelo de canal, que inclui fábricas e ouvintes, codificadores de mensagem e implementações de protocolo e transporte. Normalmente, elementos de associação e associações são implementados para permitir que os canais sejam usados pela camada de aplicativo.  
  
 A camada de canal entrega ou recebe mensagens de e para a camada de serviço e transporta essas mensagens entre pontos de extremidade. Em um cliente, a camada de canal é uma pilha de fábricas de canal que criam canais para um ponto de extremidade de rede. Em um serviço, a camada de canal é uma pilha de ouvintes de canal que aceita canais recebidos em um ponto de extremidade de rede.  
  
 Há dois tipos gerais de canais: canais de protocolo e canais de transporte. Os canais de transporte são responsáveis pela transmissão real de uma mensagem de um ponto de extremidade de rede para outro. Os canais de transporte devem ter um codificador de mensagem padrão e devem ser capazes de usar um codificador de mensagem alternativo fornecido por meio de um elemento de ligação do codificador de mensagem. Um codificador de mensagem é responsável por transformar um <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType> em uma representação de transmissão e vice-versa. Os canais de protocolo são responsáveis pela implementação de protocolos de nível SOAP (por exemplo, WS-Security ou WS-ReliableMessaging).  
  
 O requisito principal para canais de transporte e de protocolo é que eles implementam as interfaces de canal necessárias. Para criar uma camada de canal de trabalho, eles devem ter fábricas e ouvintes associados e assim por diante. Para usar as implementações de canal do WCF, é necessário haver um elemento de associação associado derivado de <xref:System.ServiceModel.Channels.BindingElement> para cada canal e deve haver uma extensão de associação relacionada para inclusão em arquivos de configuração que derivam de <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> .  
  
 Como mencionado anteriormente, os elementos de associação para codificadores de mensagens, protocolo e implementações de canal de transporte podem ser empilhados para formar uma pilha de canais e o mecanismo para conlineá-los em um conjunto ordenado é a associação. Associações e elementos de associação conectam o modelo de programação de aplicativo ao modelo de canal. Você pode usar suas implementações de canal diretamente do código, mas a menos que codificadores, transportes e protocolos sejam implementados como elementos de associação, eles não podem ser usados no modelo de programação da camada de serviço.  
  
 Para obter detalhes sobre como desenvolver canais e seus elementos de ligação, consulte [estendendo a camada de canal](extending-the-channel-layer.md).
