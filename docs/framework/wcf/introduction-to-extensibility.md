---
description: 'Saiba mais sobre: introdução à extensibilidade'
title: Introdução à extensibilidade
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], extensibility
- Windows Communication Foundation [WCF], extensibility
- extensibility [WCF]
ms.assetid: ef56c251-d63c-4b3f-944f-b0c67bfb0f68
ms.openlocfilehash: a3e614d107d2371076358f8e7786c1bb246e36eb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732833"
---
# <a name="introduction-to-extensibility"></a>Introdução à extensibilidade

O modelo de aplicativo Windows Communication Foundation (WCF) foi projetado para resolver a maior parte dos requisitos de comunicação de qualquer aplicativo distribuído. Mas há sempre cenários para os quais o modelo de aplicativo padrão e as implementações fornecidas pelo sistema não oferecem suporte. O modelo de extensibilidade do WCF destina-se a oferecer suporte a cenários personalizados, permitindo que você modifique o comportamento do sistema em todos os níveis, mesmo no ponto de substituir todo o modelo de aplicativo. Este tópico descreve as várias áreas de extensão e aponta para mais informações sobre cada uma delas.  
  
## <a name="areas-to-extend"></a>Áreas a estender  

 Você pode estender:  
  
- O tempo de execução do aplicativo. Isso estende a expedição e o processamento de mensagens para o aplicativo. Essa área também inclui a extensão do sistema de segurança, o sistema de metadados, o sistema de serialização e as associações e os elementos de associação que conectam o aplicativo ao sistema de canal subjacente.  
  
- O tempo de execução do canal e canal. Isso estende o sistema que funciona no nível de mensagem, fornecendo suporte de protocolo, transporte e codificação.  
  
- O tempo de execução do host. Isso estende a relação entre o domínio do aplicativo de hospedagem e o tempo de execução do aplicativo e do canal.  
  
### <a name="extending-the-application-runtime"></a>Estendendo o tempo de execução do aplicativo  

 Em aplicativos WCF, há uma distinção entre as mensagens que são destinadas a um canal correspondente e mensagens que são destinadas ao próprio aplicativo. As mensagens de canal dão suporte a algumas funcionalidades relacionadas ao canal, como o estabelecimento de uma conversa segura ou o estabelecimento de uma sessão confiável. Essas mensagens não estão disponíveis para o tempo de execução do aplicativo; Eles são processados antes que a camada de aplicativo esteja envolvida.  
  
 As mensagens de aplicativo contêm dados destinados a uma operação de cliente ou de serviço que você ou o cliente criou. Essas mensagens estão disponíveis para o sistema de extensão de nível de aplicativo na forma de mensagem ou de objeto, dependendo das suas necessidades.  
  
 Todas as mensagens passam pelo sistema do canal; somente as mensagens de aplicativo são passadas do sistema de canal para o aplicativo. Para criar uma nova funcionalidade de nível de canal, você deve estender o sistema do canal. Para criar uma nova funcionalidade de nível de aplicativo, você deve estender o tempo de execução do serviço ou do cliente (expatches e fábricas de canal, respectivamente). Para obter mais informações sobre como estender o tempo de execução do aplicativo, consulte [estendendo o ServiceHost e a camada do modelo de serviço](./extending/extending-servicehost-and-the-service-model-layer.md).  
  
#### <a name="extending-security"></a>Segurança estendida  

 Para criar mecanismos de segurança personalizados, como tokens e credenciais, você deve estender o sistema de segurança. Para obter mais informações, consulte [estendendo a segurança](./extending/extending-security.md).  
  
#### <a name="extending-metadata"></a>Estendendo metadados  

 Para expor seus metadados de forma diferente do padrão, você deve estender o sistema de metadados. Para obter mais informações, consulte [estendendo o sistema de metadados](./extending/extending-the-metadata-system.md).  
  
#### <a name="extending-serialization"></a>Estendendo a serialização  

 Para criar codificadores personalizados, fornecer substitutos de dados ou outro trabalho que envolva a personalização de dados transferidos, você deve estender o sistema de serialização. Para obter mais informações, consulte [estendendo codificadores e serializadores](./extending/extending-encoders-and-serializers.md).  
  
#### <a name="extending-bindings"></a>Estendendo associações  

 Para associar canais de transporte ou de protocolo à camada de aplicativo, você deve estender o sistema de associação. Para obter mais informações, consulte [estendendo associações](./extending/extending-bindings.md).  
  
### <a name="extending-the-channel-system"></a>Estendendo o sistema do canal  

 Para criar canais com suporte para transportes personalizados ou funcionalidade de protocolo, consulte [estendendo a camada de canal](./extending/extending-the-channel-layer.md).  
  
### <a name="extending-the-service-hosting-system"></a>Estendendo o sistema de Hospedagem de serviço  

 Para modificar o modelo de aplicativo de todo o serviço, você deve estender a <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType> classe. Para obter mais informações, consulte [estendendo o ServiceHost e a camada do modelo de serviço](./extending/extending-servicehost-and-the-service-model-layer.md).  
  
 Para modificar a relação entre o domínio do aplicativo de hospedagem e o host de serviço, você deve estender a <xref:System.ServiceModel.Activation.ServiceHostFactory?displayProperty=nameWithType> classe. Para obter mais informações, consulte [estendendo hospedagem usando ServiceHostFactory](./extending/extending-hosting-using-servicehostfactory.md).  
  
## <a name="see-also"></a>Consulte também

- [Estendendo o WCF](./extending/index.md)
