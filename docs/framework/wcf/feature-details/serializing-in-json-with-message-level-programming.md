---
description: 'Saiba mais sobre: serialização em JSON com programação em nível de mensagem'
title: Serialização em Json com programação de nível de mensagem
ms.date: 03/30/2017
ms.assetid: 5f940ba2-57ee-4c49-a779-957c5e7e71fa
ms.openlocfilehash: 715e44b0e2137197f5883e2327288555513f29cd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793539"
---
# <a name="serializing-in-json-with-message-level-programming"></a>Serialização em Json com programação de nível de mensagem

O WCF dá suporte à serialização de dados no formato JSON. Este tópico descreve como informar ao WCF para serializar seus tipos usando o <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> .  
  
## <a name="typed-message-programming"></a>Programação de mensagens digitadas  

 O <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> é usado quando o <xref:System.ServiceModel.Web.WebGetAttribute> ou o <xref:System.ServiceModel.Web.WebInvokeAttribute> é aplicado a uma operação de serviço. Ambos os atributos permitem que você especifique `RequestFormat` e `ResponseFormat`. Para usar JSON para solicitações e respostas. Defina ambos como `WebMessageFormat.Json` .  Para usar o JSON, você deve usar o <xref:System.ServiceModel.WebHttpBinding> , que configura automaticamente o <xref:System.ServiceModel.Description.WebHttpBehavior> . Para obter mais informações sobre a serialização do WCF, consulte [serialização e desserialização](serialization-and-deserialization.md). Para obter mais informações sobre JSON e WCF, consulte [Service Station-uma introdução aos serviços RESTful com o WCF](/archive/msdn-magazine/2009/january/service-station-an-introduction-to-restful-services-with-wcf).  
  
> [!IMPORTANT]
> O uso do JSON requer <xref:System.ServiceModel.WebHttpBinding> o uso de e <xref:System.ServiceModel.Description.WebHttpBehavior> que não oferece suporte à comunicação SOAP. Serviços que se comunicam com o não <xref:System.ServiceModel.WebHttpBinding> dão suporte à exposição de metadados de serviço, portanto, você não poderá usar a funcionalidade de Adicionar referência de serviço do Visual Studio ou a ferramenta de linha de comando svcutil para gerar um proxy do lado do cliente. Para obter mais informações sobre como chamar programaticamente os serviços que usam <xref:System.ServiceModel.WebHttpBinding> o, consulte [como consumir serviços REST com o WCF](/archive/blogs/pedram/how-to-consume-rest-services-with-wcf).  
  
## <a name="untyped-message-programming"></a>Programação de mensagens não tipadas  

 Ao trabalhar diretamente com objetos de mensagem não tipados, você deve definir explicitamente as propriedades na mensagem não tipada para serializá-la como JSON. O trecho de código a seguir mostra como fazer isso.  
  
```csharp
 Message response = Message.CreateMessage(  
                  MessageVersion.None,    // No SOAP message version  
                             "*",                     // SOAP action, ignored since this is JSON  
                             "Response string: JSON format specified", // Message body  
                             new DataContractJsonSerializer(typeof(string))); // Specify DataContractJsonSerializer  
      response.Properties.Add( WebBodyFormatMessageProperty.Name,
                    new WebBodyFormatMessageProperty(WebContentFormat.Json)); // Use JSON format  
```  
  
## <a name="see-also"></a>Consulte também

- [Integração de AJAX e suporte para JSON](ajax-integration-and-json-support.md)
- [Serialização JSON autônoma](stand-alone-json-serialization.md)
- [Serialização JSON](../samples/json-serialization.md)
