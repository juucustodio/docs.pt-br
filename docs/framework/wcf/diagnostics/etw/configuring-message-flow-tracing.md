---
description: 'Saiba mais sobre: Configurando o rastreamento de fluxo de mensagens'
title: Configurando rastreamento de fluxo de mensagem
ms.date: 03/30/2017
ms.assetid: 15571ca2-bee2-47fb-ba10-fcbc09152ad0
ms.openlocfilehash: c91362ca0d0a8fd83f69c6988d2ad2786b08b339
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798843"
---
# <a name="configuring-message-flow-tracing"></a>Configurando rastreamento de fluxo de mensagem

Quando o rastreamento de atividade de Windows Communication Foundation (WCF) está habilitado, as IDs de atividade de ponta a ponta são atribuídas a atividades lógicas em toda a pilha do WCF. No [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] , agora há uma versão de desempenho mais alta desse recurso que funciona com o ETW (rastreamento de eventos para Windows) chamado rastreamento de fluxo de mensagens. Quando habilitado, as IDs de atividade de ponta a ponta são obtidas de mensagens de entrada (ou atribuídas a se estiverem vazias) e são propagadas para todos os eventos de rastreamento emitidos depois que a mensagem é decodificada pelo canal. Os clientes podem usar esse recurso para reconstruir fluxos de mensagens com logs de rastreamento de diferentes serviços após a decodificação.  
  
 O rastreamento pode ser habilitado depois que um problema é detectado com o aplicativo e desabilitado quando o problema é resolvido.  
  
## <a name="enabling-tracing"></a>Habilitar o rastreamento  

 Você pode habilitar o rastreamento de fluxo de mensagens definindo o elemento de configuração .NET Framework 4 como `messageFlowTracing` `true` , conforme mostrado no exemplo a seguir.  
  
```xml  
<system.servicemodel>  
  <diagnostics>  
    <endToEndTracing propagateActivity="true" messageFlowTracing="true" />  
  </diagnostics>  
</system.servicemodel>  
```  
  
> [!NOTE]
> Como o `endToEndTracing` elemento de configuração reside em um arquivo de Web.config, ele não pode ser configurado dinamicamente da mesma maneira que o ETW. Para que o `endToEndTracing` elemento de configuração entre em vigor, o aplicativo deve ser reciclado.  
  
 As atividades são correlacionadas pelo intercâmbio de um identificador chamado ID da atividade. Esse identificador é um GUID e é gerado pela classe System. Diagnostics. CorrelationManager. Se você manipular System. Diagnostics. Trace. CorrelationManager. ActivityId, verifique se o valor está definido como original quando o controle de execução transfere de volta para o código WCF.  Além disso, se você usar um modelo de programação assíncrono do WCF, certifique-se de que System. Diagnostics. Trace. CorrelationManager. ActivityId seja transferido entre os threads.  
  
## <a name="message-flow-tracing-and-rest-services"></a>Rastreamento de fluxo de mensagens e serviços REST  

 O rastreamento de fluxo de mensagens permite que você rastreie uma solicitação de ponta a ponta.  Com os serviços baseados em SOAP, uma ID de atividade é enviada em um cabeçalho de mensagem SOAP. As solicitações REST não contêm esse cabeçalho, portanto, um cabeçalho de evento HTTP especial é usado. O trecho de código a seguir mostra como você pode recuperar programaticamente o valor da ID da atividade:  
  
```csharp
Object output = null;
if (OperationContext.Current.IncomingMessageProperties.TryGetValue(HttpRequestMessageProperty.Name, out output))
{
   HttpRequestMessageProperty httpHeaders = output as HttpRequestMessageProperty;
   // Retrieve the Activity Id from the HTTP header    string e2eId = httpHeaders.Headers["E2EActivity"];
   // ...
}
```

 Você pode adicionar o cabeçalho programaticamente usando o seguinte código:  
  
```csharp  
HttpContent content = new StreamContent(contentStream);  
Guid correlation = Guid.NewGuid();  
content.Headers.Add("E2EActivity", Convert.ToBase64String(correlation.ToByteArray()));  
```
