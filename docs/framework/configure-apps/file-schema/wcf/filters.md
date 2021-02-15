---
description: 'Saiba mais sobre: <filters>'
title: <filters>
ms.date: 03/30/2017
ms.assetid: 37a87222-ec78-4728-8105-9ca1bd961f0c
ms.openlocfilehash: c66dd07c91e78d1ae6e10790014c3d1b25e5538d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99664594"
---
# \<filters>

O `filters` elemento contém uma coleção de filtros XPath usados para controlar que tipo de mensagem é registrada.

Os filtros são aplicados somente na camada de transporte, especificada por `logMessagesAtTransportLevel` is `true` . O nível de serviço e o log de mensagens malformados não são afetados por filtros.

Para adicionar um filtro à coleção, use a `add` palavra-chave. Quando um ou mais filtros são definidos, somente as mensagens que correspondem a pelo menos um dos filtros são registradas. Se nenhum filtro for definido, todas as mensagens passarão.

Os filtros dão suporte à sintaxe XPath completa e são aplicados na ordem em que aparecem no arquivo de configuração. Um filtro sintaticamente incorreto resulta em uma exceção de configuração.

Veja a seguir um exemplo de como configurar um filtro que registra somente as mensagens que têm uma seção de cabeçalho SOAP.
  
```xml  
<messageLogging logEntireMessage="true"
                logMalformedMessages="true"
                logMessagesAtServiceLevel="true"
                logMessagesAtTransportLevel="true"
                maxMessagesToLog="420">
  <filters>
    <add xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
      /soap:Envelope/soap:Headers
    </add>
  </filters>
</messageLogging>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.DiagnosticSection>
- <xref:System.ServiceModel.Diagnostics>
- <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement.Filters%2A>
- <xref:System.ServiceModel.Configuration.XPathMessageFilterElementCollection>
- <xref:System.ServiceModel.Configuration.XPathMessageFilterElement>
- <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>
- [Configurando registros de mensagens em log](../../../wcf/diagnostics/configuring-message-logging.md)
- [\<messageLogging>](messagelogging.md)
