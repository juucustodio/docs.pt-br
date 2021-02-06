---
description: 'Saiba mais sobre: estendendo o WCF'
title: Estendendo o WCF
ms.date: 03/30/2017
helpviewer_keywords:
- WCF, extensibility
- extensibility [WCF]
- Windows Communication Foundation, extensibility
ms.assetid: c145e2f6-f402-41f5-8b5a-eee03978737b
ms.openlocfilehash: e243e03a72e6530716959499c311bfe37a39b054
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644145"
---
# <a name="extending-wcf"></a>Estendendo o WCF

O Windows Communication Foundation (WCF) permite que você modifique e estenda os componentes de tempo de execução para controlar e estender precisamente os aplicativos baseados em serviço. Os tópicos nesta seção se aprofundam em detalhes sobre a arquitetura de extensibilidade. Para obter mais informações sobre programação básica, consulte [programação básica do WCF](../basic-wcf-programming.md).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Estendendo a camada de modelo de serviço e o ServiceHost](extending-servicehost-and-the-service-model-layer.md)  
 A camada do modelo de serviço é responsável por extrair mensagens de entrada dos canais subjacentes, traduzi-las em invocações de método no código do aplicativo e enviar os resultados de volta para o chamador.  As extensões de modelo de serviço modificam ou implementam o comportamento de execução ou de comunicação e recursos que envolvem a funcionalidade do Dispatcher, comportamentos personalizados, interceptação de mensagem e de parâmetro e outras funcionalidades de extensibilidade.  
  
 [Estendendo associações](extending-bindings.md)  
 Associações são objetos que descrevem os detalhes de comunicação necessários para se conectar a um ponto de extremidade. Extensões de associação ou associações personalizadas implementam a funcionalidade de comunicação personalizada necessária para dar suporte aos recursos do aplicativo.  
  
 [Estendendo a camada do canal](extending-the-channel-layer.md)  
 A camada de canal fica abaixo da camada de modelo de serviço e é responsável pela troca de mensagens entre clientes e serviços. As extensões de canal podem implementar a nova funcionalidade de protocolo, como segurança. As extensões de canal também transportam a funcionalidade, como a implementação de um novo transporte de rede para transportar mensagens SOAP.  
  
 [Segurança estendida](extending-security.md)  
 A segurança no WCF consiste em segurança de transferência (integridade, confidencialidade e autenticação), controle de acesso (autorização) e auditoria. As classes encontradas no `IdentityModel` namespace são usadas pelo WCF para controle de acesso. Entender a arquitetura de segurança permite que você crie tipos de declaração personalizados para acomodar sistemas de controle de acesso personalizados.  
  
 [Estendendo o sistema de metadados](extending-the-metadata-system.md)  
 O sistema de metadados do WCF é um grupo de classes e interfaces que representam os metadados necessários para implementar aplicativos baseados em serviço. Modifique ou estenda as classes ou implemente e configure as interfaces para exportar e importar metadados personalizados, como extensões WSDL (Web Services Description Language) ou declarações de WS-PolicyAttachments personalizadas.  
  
 [Estendendo codificadores e serializadores](extending-encoders-and-serializers.md)  
 Codificadores e serializadores convertem dados de um formulário para outro. Os tópicos nesta seção discutem como estender as classes fornecidas para atender aos requisitos especiais.  
  
## <a name="reference"></a>Referência  

 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Description>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Selectors>  
  
 <xref:System.IdentityModel.Tokens>  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Programação de WCF básica](../basic-wcf-programming.md)  
  
 [Detalhes de funcionalidades do WCF](../feature-details/index.md)  
  
 [Diretrizes e práticas recomendadas](../guidelines-and-best-practices.md)
