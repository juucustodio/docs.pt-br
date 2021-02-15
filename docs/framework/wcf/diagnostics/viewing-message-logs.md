---
description: 'Saiba mais sobre: Exibindo logs de mensagens'
title: Visualizando logs de mensagem
ms.date: 03/30/2017
ms.assetid: 3012fa13-f650-45fb-aaea-c5cca8c7d372
ms.openlocfilehash: c640b2c3793839be4a31123701865fa944eaebc8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99758028"
---
# <a name="viewing-message-logs"></a>Visualizando logs de mensagem

Este tópico descreve como você pode exibir logs de mensagens.  
  
## <a name="viewing-message-logs-in-the-service-trace-viewer"></a>Exibindo logs de mensagens no Visualizador de rastreamento de serviço  

 Uma mensagem será transformada conforme é processada pelo WCF. Portanto, uma mensagem que está sendo registrada reflete apenas o conteúdo da mensagem no ponto em que foi registrado, não o conteúdo na conexão.  
  
 Como a saída do log de mensagens não tem nenhuma relação com o formato de transferência da mensagem, o log de mensagens sempre gera a mensagem decodificada. Se você configurou o log de mensagens corretamente, qualquer mensagem registrada deverá estar em texto sem formatação. Por exemplo, o formato (texto sem formatação) das mensagens registradas não é afetado pelo uso de um codificador de mensagem binária.  
  
 A saída de XmlWriterTraceListener é um arquivo que contém uma sequência de fragmentos XML. Você deve estar ciente de que o arquivo não é um arquivo XML válido. É recomendável que você use a [ferramenta do Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) para exibir os arquivos de log de mensagens. Para obter mais informações sobre como usar essa ferramenta, consulte [usando o Visualizador de rastreamento de serviço para exibir rastreamentos correlacionados e solução de problemas](./tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
 No Visualizador de rastreamento de serviço, as mensagens são listadas na guia **mensagem** . As mensagens que ocorreram ou estão relacionadas a um erro de processamento são realçadas em amarelo (nível de aviso) ou vermelho (nível de erro), dependendo da severidade do erro. Clicar duas vezes na mensagem abre o rastreamento de mensagem no contexto da solicitação de processamento.  
  
> [!NOTE]
> Se uma mensagem não tiver cabeçalho, nenhuma `<header/>` marca será registrada.  
  
## <a name="viewing-messages-logged-by-a-client-a-relay-and-a-service"></a>Exibindo mensagens registradas por um cliente, uma retransmissão e um serviço  

 Seu ambiente pode conter um cliente, que envia uma mensagem para uma retransmissão, que, posteriormente, encaminha a mensagem para o serviço. Quando o log de mensagens é habilitado em todos os três locais e todos os três logs de mensagens são exibidos na [ferramenta Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) simultaneamente, as trocas de log de mensagens serão processadas incorretamente. Isso ocorre porque o `CorrelationId` e `ActivityId` no cabeçalho da mensagem não são exclusivos para todos os pares de envio-recebimento.  
  
 Você pode usar qualquer um dos métodos a seguir para resolver esse problema.  
  
- Apenas exiba dois dos três logs de mensagem na [ferramenta do Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) a qualquer momento.  
  
- Se você precisar exibir todos os três logs na [ferramenta Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) ao mesmo tempo, poderá modificar o serviço de retransmissão criando uma nova <xref:System.ServiceModel.Channels.Message> instância. Essa instância deve ser uma cópia do corpo da mensagem de entrada, além de todos os cabeçalhos, exceto os `ActivityId` `Action` cabeçalhos e. O código de exemplo a seguir demonstra como fazer isso.  
  
```csharp
Message outgoingMessage = Message.CreateMessage(incomingMessage.Version, incomingMessage.Headers.Action, incomingMessage.GetReaderAtBodyContents());  
  
for (int i = 0; i < incomingMessage.Headers.Count; i++)  
{  
   if (incomingMessage.Headers[i].Name.Equals("ActivityId", StringComparison.InvariantCultureIgnoreCase) ||  
incomingMessage.Headers[i].Name.Equals("Action", StringComparison.InvariantCultureIgnoreCase))  
   {  
      continue;  
    }  
    outgoingMessage.Headers.CopyHeaderFrom(incomingMessage, i);  
}  
```  
  
## <a name="exceptional-cases-for-inaccurate-message-logging-content"></a>Casos excepcionais para conteúdo de log de mensagens imprecisos  

 Sob as condições a seguir, as mensagens sendo registradas podem não ser a representação exata do fluxo de octetos presentes na conexão.  
  
- Para BasicHttpBinding, os cabeçalhos de envelope são registrados para as mensagens de entrada no namespace/Addressing/None.  
  
- Os espaços em branco podem ser incompatíveis.  
  
- Para mensagens de entrada, elementos vazios podem ser representados de forma diferente. Por exemplo, \<tag> \</tag> em vez de\<tag/>  
  
- Quando o log PII conhecido é desabilitado por padrão ou a configuração explícita enableLoggingKnownPii = "true".  
  
- A codificação está habilitada para transformação em UTF-8.  
  
## <a name="see-also"></a>Consulte também

- [Ferramenta Visualizador de Rastreamento de Serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md)
- [Utilizando o visualizador de rastreamento de serviço para visualização de rastreamento correlacionados e soluções de problemas](./tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)
- [Registro em log de mensagens](message-logging.md)
