---
description: 'Saiba mais sobre: como acessar um serviço WSE 3,0 com um cliente WCF'
title: Como acessar um serviço WSE 3.0 com um cliente do WCF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1f9bcd9b-8f8f-47fa-8f1e-0d47236eb800
ms.openlocfilehash: 5a117b4c3d743d783c37ed3e27e3cf11e44abec3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742921"
---
# <a name="how-to-access-a-wse-30-service-with-a-wcf-client"></a>Como acessar um serviço WSE 3.0 com um cliente do WCF

Os clientes do Windows Communication Foundation (WCF) são compatíveis de nível de conexão com o WSE (Web Services Enhancements) 3,0 para serviços de Microsoft .NET quando os clientes WCF são configurados para usar a versão de agosto de 2004 da especificação de WS-Addressing. No entanto, os serviços WSE 3,0 não dão suporte ao protocolo MEX (troca de metadados), portanto, quando você usa a [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) para criar uma classe de cliente WCF, as configurações de segurança não são aplicadas ao cliente WCF gerado. Portanto, você deve especificar as configurações de segurança que o serviço WSE 3,0 exige depois que o cliente WCF é gerado.  
  
 Você pode aplicar essas configurações de segurança usando uma associação personalizada para levar em conta os requisitos do serviço WSE 3,0 e os requisitos interoperáveis entre um serviço WSE 3,0 e um cliente WCF. Esses requisitos de interoperabilidade incluem o uso mencionado anteriormente da especificação de WS-Addressing de agosto de 2004 e a proteção de mensagem padrão do WSE 3.0 do <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt> . A proteção de mensagem padrão para WCF é <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature> . Este tópico fornece detalhes sobre como criar uma associação WCF que interopera com um serviço WSE 3,0. O WCF também fornece um exemplo que incorpora essa associação. Para obter mais informações sobre este exemplo, consulte [interoperação com serviços Web ASMX](../samples/interoperating-with-asmx-web-services.md).  
  
### <a name="to-access-a-wse-30-web-service-with-a-wcf-client"></a>Para acessar um serviço Web WSE 3,0 com um cliente WCF  
  
1. Execute a [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) para criar um cliente WCF para o serviço Web WSE 3,0.  
  
     Para um serviço Web WSE 3,0, um cliente WCF é criado. Como o WSE 3,0 não oferece suporte ao protocolo MEX, você não pode usar a ferramenta para recuperar os requisitos de segurança para o serviço Web. O desenvolvedor do aplicativo deve adicionar as configurações de segurança para o cliente.  
  
     Para obter mais informações sobre como criar um cliente WCF, consulte o [How to: criar um cliente](../how-to-create-a-wcf-client.md).  
  
2. Crie uma classe que represente uma associação que possa se comunicar com os serviços Web do WSE 3,0.  
  
     A classe a seguir faz parte da amostra [interoperação com o WSE](/previous-versions/dotnet/netframework-3.5/ms752257(v=vs.90)) :  
  
    1. Crie uma classe que derive da classe <xref:System.ServiceModel.Channels.Binding>.  
  
         O exemplo de código a seguir cria uma classe chamada `WseHttpBinding` derivada da <xref:System.ServiceModel.Channels.Binding> classe.  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2. Adicione Propriedades à classe que especifica a declaração do WSE pronto para uso pelo serviço WSE, se as chaves derivadas são necessárias, se as sessões seguras são usadas, se as confirmações de assinatura são necessárias e as configurações de proteção de mensagem. No WSE 3,0, uma declaração pronta especifica os requisitos de segurança para um cliente ou serviço Web – semelhante ao modo de autenticação de uma associação no WCF.  
  
         O exemplo de código a seguir define as `SecurityAssertion` `RequireDerivedKeys` Propriedades,, `EstablishSecurityContext` e `MessageProtectionOrder` que especificam a declaração ativada do WSE, se as chaves derivadas são necessárias, se as sessões seguras são usadas, se as confirmações de assinatura são necessárias e as configurações de proteção de mensagem, respectivamente.  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3. Substitua o <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> método para definir as propriedades de associação.  
  
         O exemplo de código a seguir especifica as configurações de transporte, codificação de mensagem e proteção de mensagem obtendo os valores das `SecurityAssertion` `MessageProtectionOrder` Propriedades e.  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3. No código do aplicativo cliente, adicione o código para definir as propriedades de associação.  
  
     O exemplo de código a seguir especifica que o cliente WCF deve usar a proteção e a autenticação de mensagens conforme definido pela declaração de segurança do WSE 3,0 pronto para uso `AnonymousForCertificate` . Além disso, as sessões seguras e as chaves derivadas são necessárias.  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir define uma associação personalizada que expõe propriedades que correspondem às propriedades de uma declaração de segurança do WSE 3,0 pronto para uso. Essa associação personalizada, que é nomeada `WseHttpBinding` , é usada para especificar as propriedades de associação para um cliente WCF que se comunica com o exemplo de início rápido do WSSECURITYANONYMOUS WSE 3,0.  

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.Binding>
- [Interoperação com o WSE](/previous-versions/dotnet/netframework-3.5/ms752257(v=vs.90))
