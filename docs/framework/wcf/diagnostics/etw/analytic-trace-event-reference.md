---
description: 'Saiba mais sobre: referência de evento de rastreamento analítico'
title: Referência de evento de rastreamento analítico
ms.date: 03/30/2017
helpviewer_keywords:
- analytic tracing [WCF]. reference
ms.assetid: e44540cf-44a1-4efc-b965-7fbfd2131d73
ms.openlocfilehash: 1f4773692d3481cd5fa662d4fc70905215939db3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798830"
---
# <a name="analytic-trace-event-reference"></a>Referência de evento de rastreamento analítico

A tabela a seguir define os níveis de evento, os identificadores e as mensagens associadas ao rastreamento analítico do WCF.  
  
## <a name="event-reference"></a>Referência de eventos  
  
|ID do evento|Evento em nível|Mensagem de evento|Palavras-chave|  
|--------------|-----------------|-------------------|--------------|  
|[131 - BufferPoolAllocation](131-bufferpoolallocation.md)|Detalhado|Alocando pool de %1 bytes.|Infraestrutura|  
|[132 - BufferPoolChangeQuota](132-bufferpoolchangequota.md)|Detalhado|BufferPool de tamanho %1, alterando a cota por %2.|Infraestrutura|  
|[133 - ActionItemScheduled](133-actionitemscheduled.md)|Detalhado|Retorno de chamada do Agendador de thread de es invocado.|Infraestrutura|  
|[134 - ActionItemCallbackInvoked](134-actionitemcallbackinvoked.md)|Detalhado|Retorno de chamada do Agendador de thread de es invocado.|Infraestrutura|  
|[201 - ClientMessageInspectorAfterReceiveInvoked](201-clientmessageinspectorafterreceiveinvoked.md)|Informações|O Dispatcher invocou ' AfterReceiveReply ' em um ClientMessageInspector do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[202 - ClientMessageInspectorBeforeSendInvoked](202-clientmessageinspectorbeforesendinvoked.md)|Informações|O Dispatcher invocou ' BeforeSendRequest ' em um ClientMessageInspector do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[203 - ClientParameterInspectorAfterCallInvoked](203-clientparameterinspectoraftercallinvoked.md)|Informações|O Dispatcher invocou ' AfterCall ' em um ClientParameterInspector. do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[204 - ClientParameterInspectorBeforeCallInvoked](204-clientparameterinspectorbeforecallinvoked.md)|Informações|O Dispatcher invocou ' BeforeCall ' em um ClientParameterInspector do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[205 - OperationInvoked](205-operationinvoked.md)|Informações|Um OperationInvoker invocou o método ' %1 '.|EndToEndMonitoring, solução de problemas, ServiceModel|  
|[206 - ErrorHandlerInvoked](206-errorhandlerinvoked.md)|Informações|O Dispatcher invocou um ErrorHandler do tipo ' %1 ' com uma exceção do tipo ' %3 '.  ErrorHandled = = ' %2 '.|Solução de problemas, ServiceModel|  
|[207 - FaultProviderInvoked](207-faultproviderinvoked.md)|Informações|O Dispatcher invocou um Faultprovider do tipo ' %1 ' com uma exceção do tipo ' %2 '.|Solução de problemas, ServiceModel|  
|[208 - MessageInspectorAfterReceiveInvoked](208-messageinspectorafterreceiveinvoked.md)|Informações|O Dispatcher invocou ' AfterReceiveReply ' em um MessageInspector do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[209 - MessageInspectorBeforeSendInvoked](209-messageinspectorbeforesendinvoked.md)|Informações|O Dispatcher invocou ' BeforeSendRequest ' em um MessageInspector do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[210 - MessageThrottleExceeded](210-messagethrottleexceeded.md)|Aviso|O limite de ' %2 ' do acelerador ' %1 ' foi atingido.|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[211 - ParameterInspectorAfterCallInvoked](211-parameterinspectoraftercallinvoked.md)|Informações|O Dispatcher invocou ' AfterCall ' em um ParameterInspector do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[212 - ParameterInspectorBeforeCallInvoked](212-parameterinspectorbeforecallinvoked.md)|Informações|O Dispatcher invocou ' BeforeCall ' em um ParameterInspector do tipo ' %1 '.|Solução de problemas, ServiceModel|  
|[213 - ServiceHostStarted](213-servicehoststarted.md)|LogAlways|ServiceHost iniciado: ' %1 '.|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[214 - OperationCompleted](214-operationcompleted.md)|Informações|Um OperationInvoker concluiu a chamada para o método ' %1 '.  A duração da chamada do método era ' %2 ' MS.|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[215 - MessageReceivedByTransport](215-messagereceivedbytransport.md)|Informações|O transporte recebeu uma mensagem de ' %1 '.|Solução de problemas, ServiceModel|  
|[216 - MessageSentByTransport](216-messagesentbytransport.md)|Informações|O transporte enviou uma mensagem para ' %1 '.|Solução de problemas, ServiceModel|  
|[217 - ClientOperationPrepared](217-clientoperationprepared.md)|Informações|O cliente está executando a operação ' %1 ' definida no contrato ' %2 '. A mensagem será enviada para ' %3 '.|Solução de problemas, ServiceModel|  
|[218 - ClientOperationCompleted](218-clientoperationcompleted.md)|Informações|O cliente concluiu a execução da operação ' %1 ' definida no contrato ' %2 '. A mensagem foi enviada para ' %3 '.|Solução de problemas, ServiceModel|  
|[219 - ServiceException](219-serviceexception.md)|Erro do|Houve uma exceção sem tratamento do tipo ' %2 ' durante o processamento da mensagem.  Exceção ToString completa: %1.|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[220 - MessageSentToTransport](220-messagesenttotransport.md)|Informações|O Dispatcher enviou uma mensagem para o transporte. ID de correlação = = ' %1 '.|EndToEndMonitoring, solução de problemas, ServiceModel|  
|[221 - MessageReceivedFromTransport](221-messagereceivedfromtransport.md)|Informações|O Dispatcher recebeu uma mensagem do transporte. ID de correlação = = ' %1 '.|EndToEndMonitoring, solução de problemas, ServiceModel|  
|[222 - OperationFailed](222-operationfailed.md)|Aviso|O método ' %1 ' lançou uma exceção sem tratamento quando invocado pelo OperationInvoker. A duração da chamada do método era ' %2 ' MS.|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[223 - OperationFaulted](223-operationfaulted.md)|Aviso|O método ' %1 ' lançou uma FaultException quando invocado pelo OperationInvoker. A duração da chamada do método era ' %2 ' MS.|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[224 - MessageThrottleAtSeventyPercent](224-messagethrottleatseventypercent.md)|Aviso|O limite de ' %2 ' do acelerador ' %1 ' está em 70%.|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[226 - IdleServicesClosed](226-idleservicesclosed.md)|LogAlways|%1 serviços ociosos fora do total %2 serviços ativados fechados.|Webhost HealthMonitoring|  
|[301 - UserDefinedErrorOccurred](301-userdefinederroroccurred.md)|Erro do|Nome: ' %1 ', referência: ' %2 ', carga: %3.|UserEvents, HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[302 - UserDefinedWarningOccurred](302-userdefinedwarningoccurred.md)|Aviso|Nome: ' %1 ', referência: ' %2 ', carga: %3.|UserEvents, HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[303 - UserDefinedInformationEventOccured](303-userdefinedinformationeventoccured.md)|Informações|Nome: ' %1 ', referência: ' %2 ', carga: %3.|UserEvents, HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|[401- StopSignPostEvent](401-stopsignpostevent.md)|Informações|Limite de atividade.|Solução de problemas|  
|[402 - StartSignpostEvent](402-startsignpostevent.md)|Informações|Limite de atividade.|Solução de problemas|  
|[403 - SuspendSignpostEvent](403-suspendsignpostevent.md)|Informações|Limite de atividade.|Solução de problemas|  
|[404 - ResumeSignpostEvent](404-resumesignpostevent.md)|Informações|Limite de atividade.|Solução de problemas|  
|[451 - MessageLogInfo](451-messageloginfo.md)|Informações|%1|Solução de problemas, WCFMessageLogging|  
|[452 - MessageLogWarning](452-messagelogwarning.md)|Aviso|%1|Solução de problemas, WCFMessageLogging|  
|[499 - TransferEmitted](499-transferemitted.md)|LogAlways|Evento de transferência emitido.|Solução de problemas, UserEvents, EndToEndMonitoring, ServiceModel, WFTracking, ServiceHost, WCFMessageLogging|  
|[501 - CompilationStart](501-compilationstart.md)|Informações|Iniciar compilação.|WebHost|  
|[502 - CompilationStop](502-compilationstop.md)|Informações|Encerrar compilação.|WebHost|  
|[503 - ServiceHostFactoryCreationStart](503-servicehostfactorycreationstart.md)|Informações|ServiceHostFactory iniciar a criação.|WebHost|  
|[504 - ServiceHostFactoryCreationStop](504-servicehostfactorycreationstop.md)|Informações|ServiceHostFactory terminar a criação.|WebHost|  
|[505 - CreateServiceHostStart](505-createservicehoststart.md)|Informações|Inicie CreateServiceHost.|WebHost|  
|[506 - CreateServiceHostStop](506-createservicehoststop.md)|Informações|Encerrar CreateServiceHost.|WebHost|  
|[507 - HostedTransportConfigurationManagerConfigInitStart](507-hostedtransportconfigurationmanagerconfiginitstart.md)|Informações|HostedTransportConfigurationManager iniciar a inicialização da configuração.|WebHost|  
|[508 - HostedTransportConfigurationManagerConfigInitStop](508-hostedtransportconfigurationmanagerconfiginitstop.md)|Informações|Inicialização da configuração do HostedTransportConfigurationManager end.|WebHost|  
|[509 - ServiceHostOpenStart](509-servicehostopenstart.md)|Informações|Inicialização da configuração do HostedTransportConfigurationManager end.|ServiceHost|  
|[510 - ServiceHostOpenStop](510-servicehostopenstop.md)|Informações|Abertura de ServiceHost concluída.|ServiceHost|  
|[513 - WebHostRequestStart](513-webhostrequeststart.md)|Informações|Solicitação recebida com o caminho virtual ' %2 ' do AppDomain ' %1 '.|WebHost|  
|[514 - WebHostRequestStop](514-webhostrequeststop.md)|Informações|WebHostRequest parar.|WebHost|  
|[601 - CBAEntryRead](601-cbaentryread.md)|Detalhado|Endereço relativo do elemento de desativação processado: ' %1 ', endereço relativo normalizado ' %2 '.||  
|[602 - CBAMatchFound](602-cbamatchfound.md)|Detalhado|A solicitação de entrada corresponde a um elemento de desativação com o endereço ' %1 '.||  
|[603 - AspNetRoutingService](603-aspnetroutingservice.md)|Detalhado|A solicitação de entrada corresponde a um serviço WCF definido na rota ASP.NET com o endereço %1.|Roteamentoservices|  
|[604 - AspNetRoute](604-aspnetroute.md)|Detalhado|Uma nova rota ASP.NET ' %1 ' com serviceType ' %2 ' e serviceHostFactoryType ' %3 ' foi adicionada.|Roteamentoservices|  
|[605 - IncrementBusyCount](605-incrementbusycount.md)|Detalhado|IncrementBusyCount chamado. Origem: %1|WebHost|  
|[606 - DecrementBusyCount](606-decrementbusycount.md)|Detalhado|DecrementBusyCount chamado. Origem: %1|WebHost|  
|[701 - ServiceChannelOpenStart](701-servicechannelopenstart.md)|Detalhado|ServiceChannelOpen iniciado.|WebHost|  
|[702 - ServiceChannelOpenStop](702-servicechannelopenstop.md)|Informações|ServiceChannelOpen concluído.|ServiceModel|  
|[703 - ServiceChannelCallStart](703-servicechannelcallstart.md)|Informações|ServiceChannelCall iniciado.|ServiceModel|  
|[704 - ServiceChannelBeginCallStart](704-servicechannelbegincallstart.md)|Informações|Chamadas assíncronas de enchannel iniciadas.|ServiceModel|  
|[706 - HttpSendMessageStart](706-httpsendmessagestart.md)|Detalhado|Início da solicitação de envio http.|HTTP|  
|[707 - HttpSendStop](707-httpsendstop.md)|Detalhado|Parada de solicitação de envio http.|HTTP|  
|[708 - HttpMessageReceiveStart](708-httpmessagereceivestart.md)|Detalhado|Mensagem recebida do transporte http.|HTTP|  
|[709 - DispatchMessageStart](709-dispatchmessagestart.md)|Informações|Distribuição de mensagem iniciada.|ServiceModel|  
|[710 - HttpContextBeforeProcessAuthentication](710-httpcontextbeforeprocessauthentication.md)|Detalhado|Inicie a autenticação para distribuição de mensagens.|ServiceModel|  
|[711 - DispatchMessageBeforeAuthorization](711-dispatchmessagebeforeauthorization.md)|Detalhado|Inicie a autorização para a expedição de mensagens.|ServiceModel|  
|[712 - DispatchMessageStop](712-dispatchmessagestop.md)|Informações|Expedição de mensagem concluída.|ServiceModel|  
|[715 - ClientChannelOpenStart](715-clientchannelopenstart.md)|Informações|Início do onchannel aberto.|ServiceModel|  
|[716 - ClientChannelOpenStop](716-clientchannelopenstop.md)|Informações|Parada aberta do onchannel.|ServiceModel|  
|[717 - HttpSendStreamedMessageStart](717-httpsendstreamedmessagestart.md)|Informações|Mensagem http enviar transmissão iniciada.|HTTP|  
|[1400 - ChannelInitializationTimeout](1400-channelinitializationtimeout.md)|Erro do|1%|ServiceModel|  
|[1401 - CloseTimeout](1401-closetimeout.md)|Erro do|1%|ServiceModel|  
|[1402 - IdleTimeout](1402-idletimeout.md)|Erro do|%1 chave do pool de conexões: %2|ServiceModel|  
|[1403 - LeaseTimeout](1403-leasetimeout.md)|Informações|%1 chave do pool de conexões: %2|ServiceModel|  
|[1405 - OpenTimeout](1405-opentimeout.md)|Erro do|%1|ServiceModel|  
|[1406 - ReceiveTimeout](1406-receivetimeout.md)|Erro do|%1|ServiceModel|  
|[1407 - SendTimeout](1407-sendtimeout.md)|Erro do|%1|ServiceModel|  
|[1409 - InactivityTimeout](1409-inactivitytimeout.md)|Informações|%1|ServiceModel|  
|[1416 - MaxReceivedMessageSizeExceeded](1416-maxreceivedmessagesizeexceeded.md)|Erro do|%1|Quota|  
|[1417 - MaxSentMessageSizeExceeded](1417-maxsentmessagesizeexceeded.md)|Erro do|%1|Quota|  
|[1418 - MaxOutboundConnectionsPerEndpointExceeded](1418-maxoutboundconnectionsperendpointexceeded.md)|Informações|%1|Quota|  
|[1419 - MaxPendingConnectionsExceeded](1419-maxpendingconnectionsexceeded.md)|Informações|%1|Quota|  
|[1420 - ReaderQuotaExceeded](1420-readerquotaexceeded.md)|Erro do|%1|Quota|  
|[1422 - NegotiateTokenAuthenticatorStateCacheExceeded](1422-negotiatetokenauthenticatorstatecacheexceeded.md)|Erro do|%1|Quota|  
|[1423 - NegotiateTokenAuthenticatorStateCacheRatio](1423-negotiatetokenauthenticatorstatecacheratio.md)|Detalhado|Negociar a taxa de cache de estado do autenticador de token: %1/%2|Quota|  
|[1424 - SecuritySessionRatio](1424-securitysessionratio.md)|Detalhado|Taxa de sessão de segurança: %1/%2|Quota|  
|[1430 - PendingConnectionsRatio](1430-pendingconnectionsratio.md)|Detalhado|Taxa de conexões pendentes: %1/%2|Quota|  
|[1431 - ConcurrentCallsRatio](1431-concurrentcallsratio.md)|Detalhado|Taxa de sessões simultâneas: %1/%2|Quota|  
|[1432 - ConcurrentSessionsRatio](1432-concurrentsessionsratio.md)|Detalhado|Taxa de sessões simultâneas: %1/%2|Quota|  
|[1433 - OutboundConnectionsPerEndpointRatio](1433-outboundconnectionsperendpointratio.md)|Detalhado|Taxa de conexões de saída por ponto de extremidade: %1/%2|Quota|  
|[1436 - PendingMessagesPerChannelRatio](1436-pendingmessagesperchannelratio.md)|Detalhado|Taxa de mensagens pendentes por canal: %1/%2|Quota|  
|[1438 - ConcurrentInstancesRatio](1438-concurrentinstancesratio.md)|Detalhado|Taxa de instâncias simultâneas: %1/%2|Quota|  
|[1439 - PendingAcceptsAtZero](1439-pendingacceptsatzero.md)|Informações|Zero aceitações pendentes restantes|Quota|  
|[1441 - MaxSessionSizeReached](1441-maxsessionsizereached.md)|Aviso|1%|Quota|  
|[1442 - ReceiveRetryCountReached](1442-receiveretrycountreached.md)|Aviso|Contagem de repetições de recebimento atingida na mensagem do MSMQ com a ID ' %1 '|Quota|  
|[1443 - MaxRetryCyclesExceededMsmq](1443-maxretrycyclesexceededmsmq.md)|Erro do|Ciclos máximos de repetição excedidos na mensagem do MSMQ com a ID ' %1 '|Quota|  
|[1445 - ReadPoolMiss](1445-readpoolmiss.md)|Detalhado|Novo ' %1 ' criado|Quota|  
|[1446 - WritePoolMiss](1446-writepoolmiss.md)|Detalhado|Novo ' %1 ' criado|Quota|  
|[1451 - MaxRetryCyclesExceeded](1451-maxretrycyclesexceeded.md)|Erro do|1%|Quota|  
|[3300 - ReceiveContextCompleteFailed](3300-receivecontextcompletefailed.md)|Aviso|Falha ao concluir %1.|Canal|  
|[3301 - ReceiveContextAbandonFailed](3301-receivecontextabandonfailed.md)|Aviso|Falha ao abandonar %1.|Canal|  
|[3303 - ReceiveContextAbandonWithException](3303-receivecontextabandonwithexception.md)|Aviso|Falha no contexto de recebimento.|ServiceModel|  
|[3303 - ReceiveContextAbandonWithException](3303-receivecontextabandonwithexception.md)|Informações|%1 foi abandonado com a exceção %2.|Canal|  
|[3305 - ClientBaseCachedChannelFactoryCount](3305-clientbasecachedchannelfactorycount.md)|Informações|O número de fábricas de canal em cache é: ' %1 '.  No máximo ' %2 ' fábricas de canais podem ser armazenadas em cache.|ServiceModel|  
|[3306 - ClientBaseChannelFactoryAgedOutofCache](3306-clientbasechannelfactoryagedoutofcache.md)|Informações|Uma fábrica de canais esteve antiga fora do cache porque o cache atingiu seu limite de ' %1 '.|ServiceModel|  
|[3307 - ClientBaseChannelFactoryCacheHit](3307-clientbasechannelfactorycachehit.md)|Informações|Fábrica de canais correspondente usada encontrada no cache.|ServiceModel|  
|[3308 - ClientBaseUsingLocalChannelFactory](3308-clientbaseusinglocalchannelfactory.md)|Informações|Não usar a fábrica de canais do cache, ou seja, o Caching desabilitado por exemplo.|ServiceModel|  
|[3309 - QueryCompositionExecuted](3309-querycompositionexecuted.md)|Informações|A composição de consulta usando ' %1 ' foi executada no URI de solicitação: ' %2 '.|ServiceModel|  
|[3310 - DispatchFailed](3310-dispatchfailed.md)|Erro do|A operação ' %1 ' foi expedida com erros.|ServiceModel|  
|[3311 - DispatchSuccessful](3311-dispatchsuccessful.md)|Informações|A operação ' %1 ' foi expedida com êxito.|ServiceModel|  
|[3312 - MessageReadByEncoder](3312-messagereadbyencoder.md)|Informações|Uma mensagem com o tamanho ' %1 ' bytes foi lida pelo codificador.|Canal|  
|[3312 - MessageReadByEncoder](3312-messagereadbyencoder.md)|Informações|Uma mensagem com tamanho de ' %1 ' bytes foi gravada pelo codificador.|Canal|  
|[3314 - SessionIdleTimeout](3314-sessionidletimeout.md)|Erro do|Anulando sessão para o canal ocioso para o URI: ' %1 '.|ServiceModel|  
|[3319 - SocketAcceptEnqueued](3319-socketacceptenqueued.md)|Detalhado|Aceitação de conexão iniciada.|TCP|  
|[3320 - SocketAccepted](3320-socketaccepted.md)|Detalhado|Listenerid: %1 aceitou Socketid: %2.|TCP|  
|[3321 - ConnectionPoolMiss](3321-connectionpoolmiss.md)|Detalhado|O pool para %1 não tem conexão disponível e %2 conexões ocupadas.|Canal|  
|[3322 - DispatchFormatterDeserializeRequestStart](3322-dispatchformatterdeserializerequeststart.md)|Detalhado|O Dispatcher iniciou a desserialização da mensagem de solicitação.|ServiceModel|  
|[3323 - DispatchFormatterDeserializeRequestStop](3323-dispatchformatterdeserializerequeststop.md)|Detalhado|O Dispatcher concluiu a desserialização da mensagem de solicitação.|ServiceModel|  
|[3324 - DispatchFormatterSerializeReplyStart](3324-dispatchformatterserializereplystart.md)|Detalhado|O Dispatcher iniciou a serialização da mensagem de resposta.|ServiceModel|  
|[3325 - DispatchFormatterSerializeReplyStop](3325-dispatchformatterserializereplystop.md)|Detalhado|O Dispatcher concluiu a serialização da mensagem de resposta.|ServiceModel|  
|[3326 - ClientFormatterSerializeRequestStart](3326-clientformatterserializerequeststart.md)|Detalhado|Serialização de solicitação do cliente iniciada.|ServiceModel|  
|[3327 - ClientFormatterSerializeRequestStop](3327-clientformatterserializerequeststop.md)|Detalhado|O cliente concluiu a serialização da mensagem de solicitação.|ServiceModel|  
|[3328 - ClientFormatterDeserializeReplyStart](3328-clientformatterdeserializereplystart.md)|Detalhado|O cliente iniciou a desserialização da mensagem de resposta.|ServiceModel|  
|[3329 - ClientFormatterDeserializeReplyStop](3329-clientformatterdeserializereplystop.md)|Detalhado|O cliente concluiu a desserialização da mensagem de resposta.|ServiceModel|  
|[3330 - SecurityNegotiationStart](3330-securitynegotiationstart.md)|Detalhado|Negociação de segurança iniciada.|Segurança|  
|[3331 - SecurityNegotiationStop](3331-securitynegotiationstop.md)|Detalhado|Negociação de segurança concluída.|Segurança|  
|[3332 - SecurityTokenProviderOpened](3332-securitytokenprovideropened.md)|Detalhado|Abertura de SecurityTokenprovider concluída.|Segurança|  
|[3333 - OutgoingMessageSecured](3333-outgoingmessagesecured.md)|Detalhado|A mensagem de saída foi protegida.|Segurança|  
|[3334 - IncomingMessageVerified](3334-incomingmessageverified.md)|Detalhado|A mensagem de entrada foi verificada.|ServiceModel de segurança|  
|[3335 - GetServiceInstanceStart](3335-getserviceinstancestart.md)|Detalhado|Recuperação da instância de serviço iniciada.|ServiceModel|  
|[3336 - GetServiceInstanceStop](3336-getserviceinstancestop.md)|Detalhado|Instância de serviço recuperada.|ServiceModel|  
|[3337 - ChannelReceiveStart](3337-channelreceivestart.md)|Detalhado|ChannelHandlerId: %1-loop de recebimento de mensagem iniciado.|Canal|  
|[3338 - ChannelReceiveStop](3338-channelreceivestop.md)|Detalhado|ChannelHandlerId: %1-loop de recebimento de mensagem interrompido.|Canal|  
|[3339 - ChannelFactoryCreated](3339-channelfactorycreated.md)|Detalhado|ChannelFactory criada.|ServiceModel|  
|[3340 - PipeConnectionAcceptStart](3340-pipeconnectionacceptstart.md)|Detalhado|Aceitação de conexão de pipe iniciada em %1.|Canal|  
|[3341 - PipeConnectionAcceptStop](3341-pipeconnectionacceptstop.md)|Detalhado|Conexão de pipe aceita.|Canal|  
|[3342 - EstablishConnectionStart](3342-establishconnectionstart.md)|Detalhado|Estabelecimento de conexão iniciado para %1.|Canal|  
|[3343 - EstablishConnectionStop](3343-establishconnectionstop.md)|Detalhado|Conexão estabelecida.|Canal|  
|[3345 - SessionPreambleUnderstood](3345-sessionpreambleunderstood.md)|Detalhado|Preâmbulo de sessão para ' %1 ' compreendido.|Canal|  
|[3346 - ConnectionReaderSendFault](3346-connectionreadersendfault.md)|Erro do|Falha no envio do leitor de conexão ' %1 '.|Canal|  
|[3347 - SocketAcceptClosed](3347-socketacceptclosed.md)|Detalhado|Aceitação de soquete fechada.|TCP|  
|[3348 - ServiceHostFaulted](3348-servicehostfaulted.md)|Crítico|Falha no host de serviço.|TCP|  
|[3349 - ListenerOpenStart](3349-listeneropenstart.md)|Detalhado|Abertura de ouvinte para ' %1 '.|Canal|  
|[3350 - ListenerOpenStop](3350-listeneropenstop.md)|Detalhado|Abertura de ouvinte concluída.|Canal|  
|[3351 - ServerMaxPooledConnectionsQuotaReached](3351-servermaxpooledconnectionsquotareached.md)|Detalhado|Cota máxima de conexões em pool do servidor atingida.|Quota|  
|[3352 - TcpConnectionTimedOut](3352-tcpconnectiontimedout.md)|Erro do|Socketid: %1 para o endereço remoto %2 atingiu o tempo limite.|TCP|  
|[3353 - TcpConnectionResetError](3353-tcpconnectionreseterror.md)|Aviso|Socketid: %1 para o endereço remoto %2 teve um erro de redefinição de conexão.|TCP|  
|[3354 - ServiceSecurityNegotiationCompleted](3354-servicesecuritynegotiationcompleted.md)|Detalhado|Negociação de segurança de serviço concluída.|Segurança|  
|[3355 - SecurityNegotiationProcessingFailure](3355-securitynegotiationprocessingfailure.md)|Erro do|Falha no processamento da negociação de segurança.|Segurança|  
|[3356 - SecurityIdentityVerificationSuccess](3356-securityidentityverificationsuccess.md)|Detalhado|Verificação de segurança bem-sucedida.|Segurança|  
|[3357 - SecurityIdentityVerificationFailure](3357-securityidentityverificationfailure.md)|Erro do|Falha na verificação de segurança.|Segurança|  
|[3358 - PortSharingDuplicatedSocket](3358-portsharingduplicatedsocket.md)|Detalhado|Soquete duplicado para %1.|Ativaçãoservices|  
|[3359 - SecurityImpersonationSuccess](3359-securityimpersonationsuccess.md)|Detalhado|Representação de segurança bem-sucedida.|Segurança|  
|[3360 - SecurityImpersonationFailure](3360-securityimpersonationfailure.md)|Aviso|Falha na representação de segurança.|Segurança|  
|[3361 - HttpChannelRequestAborted](3361-httpchannelrequestaborted.md)|Aviso|Solicitação de canal http anulada.|HTTP|  
|[3362 - HttpChannelResponseAborted](3362-httpchannelresponseaborted.md)|Aviso|Resposta de canal http anulada.|HTTP|  
|[3363 - HttpAuthFailed](3363-httpauthfailed.md)|Aviso|Falha na autenticação http.|HTTP|  
|[3364 - SharedListenerProxyRegisterStart](3364-sharedlistenerproxyregisterstart.md)|Detalhado|Registro de SharedListenerProxy iniciado para o URI ' %1 '.|Ativaçãoservices|  
|[3365 - SharedListenerProxyRegisterStop](3365-sharedlistenerproxyregisterstop.md)|Detalhado|Parar registro de SharedListenerProxy.|Ativaçãoservices|  
|[3366 - SharedListenerProxyRegisterFailed](3366-sharedlistenerproxyregisterfailed.md)|Erro do|Falha no registro de SharedListenerProxy com o status ' %1 '.|Ativaçãoservices|  
|[3367 - ConnectionPoolPreambleFailed](3367-connectionpoolpreamblefailed.md)|Erro do|ConnectionPoolPreambleFailed.|Canal|  
|[3368 - SslOnInitiateUpgrade](3368-ssloninitiateupgrade.md)|Detalhado|SslOnAcceptUpgradeStart|Segurança|  
|[3369 - SslOnAcceptUpgrade](3369-sslonacceptupgrade.md)|Detalhado|SslOnAcceptUpgradeStop|Segurança|  
|[3370 - BinaryMessageEncodingStart](3370-binarymessageencodingstart.md)|Detalhado|BinaryMessageEncoder iniciou a codificação da mensagem.|Canal|  
|[3371 - MtomMessageEncodingStart](3371-mtommessageencodingstart.md)|Detalhado|MtomMessageEncoder iniciou a codificação da mensagem.|Canal|  
|[3372 - TextMessageEncodingStart](3372-textmessageencodingstart.md)|Detalhado|TextMessageEncoder iniciou a codificação da mensagem.|Canal|  
|[3373 - BinaryMessageDecodingStart](3373-binarymessagedecodingstart.md)|Detalhado|BinaryMessageEncoder iniciou a decodificação da mensagem.|Canal|  
|[3374 - MtomMessageDecodingStart](3374-mtommessagedecodingstart.md)|Detalhado|MtomMessageEncoder iniciou a decodificação da mensagem.|Canal|  
|[3375 - TextMessageDecodingStart](3375-textmessagedecodingstart.md)|Detalhado|TextMessageEncoder iniciou a decodificação da mensagem.|Canal|  
|[3376 - HttpResponseReceiveStart](3376-httpresponsereceivestart.md)|Informações|O transporte http iniciou o recebimento de uma mensagem.|HTTP|  
|[3377 - SocketReadStop](3377-socketreadstop.md)|Detalhado|Socketid: %1 ler ' %2 ' bytes lidos de ' %3 '.|TCP|  
|[3378 - SocketAsyncReadStop](3378-socketasyncreadstop.md)|Detalhado|Socketid: %1 ler ' %2 ' bytes lidos de ' %3 '.|TCP|  
|[3379 - SocketWriteStart](3379-socketwritestart.md)|Detalhado|Socketid: %1 gravando ' %2 ' bytes em ' %3 '.|TCP|  
|[3380 - SocketAsyncWriteStart](3380-socketasyncwritestart.md)|Detalhado|Socketid: %1 gravando ' %2 ' bytes em ' %3 '.|TCP|  
|[3381 - SequenceAcknowledgementSent](3381-sequenceacknowledgementsent.md)|Detalhado|SessionId: %1 confirmação enviada.|Canal|  
|[3382 - ClientReliableSessionReconnect](3382-clientreliablesessionreconnect.md)|Informações|SessionId: %1 reconectando.|Canal|  
|[3383 - ReliableSessionChannelFaulted](3383-reliablesessionchannelfaulted.md)|Informações|SessionId: %1 falhou.|Canal|  
|[3384 - WindowsStreamSecurityOnInitiateUpgrade](3384-windowsstreamsecurityoninitiateupgrade.md)|Detalhado|Windowsstreamsecurity está iniciando atualização de segurança.|Segurança|  
|[3385 - WindowsStreamSecurityOnAcceptUpgrade](3385-windowsstreamsecurityonacceptupgrade.md)|Detalhado|Segurança de streaming do Windows ao aceitar atualização.|Segurança|  
|[3386 - SocketConnectionAbort](3386-socketconnectionabort.md)|Aviso|Socketid: %1 está sendo anulado.|TCP|  
|[3388 - HttpGetContextStart](3388-httpgetcontextstart.md)|Detalhado|HttpGetContext iniciar.|HTTP|  
|[3389 - ClientSendPreambleStart](3389-clientsendpreamblestart.md)|Detalhado|Início do envio do preâmbulo pelo cliente.|Canal|  
|[3390 - ClientSendPreambleStop](3390-clientsendpreamblestop.md)|Detalhado|Parada do envio do preâmbulo pelo cliente.|Canal|  
|[3391 - HttpMessageReceiveFailed](3391-httpmessagereceivefailed.md)|Aviso|Falha no recebimento da mensagem http.|HTTP|  
|[3392 - TransactionScopeCreate](3392-transactionscopecreate.md)|Informações|TransactionScope está sendo criado com LocalIdentifier: ' %1 ' e DistributedIdentifier: ' %2 '.|ServiceModel|  
|[3393 - StreamedMessageReadByEncoder](3393-streamedmessagereadbyencoder.md)|Informações|Uma mensagem em fluxo foi lida pelo codificador.|Canal|  
|[3394 - StreamedMessageWrittenByEncoder](3394-streamedmessagewrittenbyencoder.md)|Informações|Uma mensagem em fluxo foi escrita pelo codificador.|Canal|  
|[3395 - MessageWrittenAsynchronouslyByEncoder](3395-messagewrittenasynchronouslybyencoder.md)|Informações|Uma mensagem foi gravada de forma assíncrona pelo codificador.|Canal|  
|[3396 - BufferedAsyncWriteStart](3396-bufferedasyncwritestart.md)|Informações|Bufferid: %1 concluiu a gravação de ' %2 ' bytes no fluxo subjacente.|Canal|  
|[3397 - BufferedAsyncWriteStop](3397-bufferedasyncwritestop.md)|Informações|Uma mensagem foi gravada de forma assíncrona pelo codificador.|Canal|  
|[3398 - PipeSharedMemoryCreated](3398-pipesharedmemorycreated.md)|Detalhado|Memória compartilhada de pipe criada em ' %1 '.|Canal|  
|[3399 - NamedPipeCreated](3399-namedpipecreated.md)|Detalhado|NamedPipe ' %1 ' criado.|Canal|  
|[3401 - SignatureVerificationStart](3401-signatureverificationstart.md)|Detalhado|Verificação de assinatura iniciada.|Segurança|  
|[3402 - SignatureVerificationSuccess](3402-signatureverificationsuccess.md)|Detalhado|Verificação de assinatura bem-sucedida.|Segurança|  
|[3403 - WrappedKeyDecryptionStart](3403-wrappedkeydecryptionstart.md)|Detalhado|Descriptografia de chave encapsulada iniciada.|Segurança|  
|[3404 - WrappedKeyDecryptionSuccess](3404-wrappedkeydecryptionsuccess.md)|Detalhado|Descriptografia de chave encapsulada bem-sucedida.|Segurança|  
|[3405 - EncryptedDataProcessingStart](3405-encrypteddataprocessingstart.md)|Detalhado|Processamento de dados criptografados iniciado.|Segurança|  
|[3406 - EncryptedDataProcessingSuccess](3406-encrypteddataprocessingsuccess.md)|Detalhado|Processamento de dados criptografados bem-sucedido.|Segurança|  
|[3407 - HttpPipelineProcessInboundRequestStart](3407-httppipelineprocessinboundrequeststart.md)|Detalhado|O manipulador de mensagens http iniciou o processamento da solicitação de entrada.|HTTP|  
|[3408 - HttpPipelineBeginProcessInboundRequestStart](3408-httppipelinebeginprocessinboundrequeststart.md)|Detalhado|O manipulador de mensagens http iniciou o processamento da solicitação de entrada de forma assíncrona.|HTTP|  
|[3409 - HttpPipelineProcessInboundRequestStop](3409-httppipelineprocessinboundrequeststop.md)|Detalhado|O manipulador de mensagens http concluiu o processamento de uma solicitação de entrada.|HTTP|  
|[3410 - HttpPipelineFaulted](3410-httppipelinefaulted.md)|Aviso|Falha no manipulador de mensagens http.|HTTP|  
|[3411 - HttpPipelineTimeoutException](3411-httppipelinetimeoutexception.md)|Erro do|A conexão WebSocket atingiu o tempo limite.|HTTP|  
|[3412 - HttpPipelineProcessResponseStart](3412-httppipelineprocessresponsestart.md)|Detalhado|O manipulador de mensagens http iniciou o processamento da resposta.|HTTP|  
|[3413 - HttpPipelineBeginProcessResponseStart](3413-httppipelinebeginprocessresponsestart.md)|Detalhado|O manipulador de mensagens http iniciou o processamento da resposta de forma assíncrona.|HTTP|  
|[3414 - HttpPipelineProcessResponseStop](3414-httppipelineprocessresponsestop.md)|Detalhado|O manipulador de mensagens http concluiu o processamento da resposta.|HTTP|  
|[3415 - WebSocketConnectionRequestSendStart](3415-websocketconnectionrequestsendstart.md)|Detalhado|Início de envio da solicitação de conexão WebSocket para ' %1 '.|HTTP|  
|[3416 - WebSocketConnectionRequestSendStop](3416-websocketconnectionrequestsendstop.md)|Detalhado|Websocketid: %1 solicitação de conexão enviada.|HTTP|  
|[3417 - WebSocketConnectionAcceptStart](3417-websocketconnectionacceptstart.md)|Detalhado|Início da aceitação da conexão WebSocket.|HTTP|  
|[3418 - WebSocketConnectionAccepted](3418-websocketconnectionaccepted.md)|Detalhado|Websocketid: %1 conexão aceita.|HTTP|  
|[3419 - WebSocketConnectionDeclined](3419-websocketconnectiondeclined.md)|Erro do|Conexão WebSocket recusada com o código de status ' %1 '|HTTP|  
|[3420 - WebSocketConnectionFailed](3420-websocketconnectionfailed.md)|Erro do|Falha na solicitação de conexão WebSocket: ' %1 '|HTTP|  
|[3421 - WebSocketConnectionAborted](3421-websocketconnectionaborted.md)|Erro do|Websocketid: %1 conexão anulada.|HTTP|  
|[3422 - WebSocketAsyncWriteStart](3422-websocketasyncwritestart.md)|Detalhado|Websocketid: %1 gravando ' %2 ' bytes em ' %3 '.|HTTP|  
|[3423 - WebSocketAsyncWriteStop](3423-websocketasyncwritestop.md)|Detalhado|Websocketid: %1 parada de gravação assíncrona.|HTTP|  
|[3424 - WebSocketAsyncReadStart](3424-websocketasyncreadstart.md)|Detalhado|Websocketid: %1 início da leitura.|HTTP|  
|[3425 - WebSocketAsyncReadStop](3425-websocketasyncreadstop.md)|Detalhado|Websocketid: %1 ler ' %2 ' bytes de ' %3 '.|HTTP|  
|[3426 - WebSocketCloseSent](3426-websocketclosesent.md)|Detalhado|Websocketid: %1 enviando mensagem de fechamento para ' %2 ' com o status de fechamento ' %3 '.|HTTP|  
|[3427 - WebSocketCloseOutputSent](3427-websocketcloseoutputsent.md)|Detalhado|Websocketid: %1 enviando mensagem de saída de fechamento para ' %2 ' com o status de fechamento ' %3 '.|HTTP|  
|[3428 - WebSocketConnectionClosed](3428-websocketconnectionclosed.md)|Detalhado|Websocketid: %1 conexão fechada.|HTTP|  
|[3429 - WebSocketCloseStatusReceived](3429-websocketclosestatusreceived.md)|Detalhado|Websocketid: %1 mensagem de fechamento de conexão recebida com o status ' %2 '.|HTTP|  
|[3430 - WebSocketUseVersionFromClientWebSocketFactory](3430-websocketuseversionfromclientwebsocketfactory.md)|Detalhado|Usando o WebSocketVersion de uma fábrica de WebSocket de cliente do tipo ' %1 '.|HTTP|  
|[3431 - WebSocketCreateClientWebSocketWithFactory](3431-websocketcreateclientwebsocketwithfactory.md)|Detalhado|Criando o WebSocket do cliente com uma fábrica do tipo ' %1 '.|HTTP|  
|[3553 - XamlServicesLoadStart](3553-xamlservicesloadstart.md)|Informações|XamlServicesLoad iniciar|WebHost|  
|[3554 - XamlServicesLoadStop](3554-xamlservicesloadstop.md)|Informações|XamlServicesLoad parar|WebHost|  
|[3555 - CreateWorkflowServiceHostStart](3555-createworkflowservicehoststart.md)|Informações|Início de CreateWorkflowServiceHost|WebHost|  
|[3556 - CreateWorkflowServiceHostStop](3556-createworkflowservicehoststop.md)|Informações|Parada de CreateWorkflowServiceHost|WebHost|  
|[3558 - ServiceActivationStart](3558-serviceactivationstart.md)|Informações|Início da ativação do serviço|WebHost|  
|[3559 - ServiceActivationStop](3559-serviceactivationstop.md)|Informações|Parada de ativação do serviço|WebHost|  
|[3560 - ServiceActivationAvailableMemory](3560-serviceactivationavailablememory.md)|Detalhado|Memória disponível (bytes): %1|Quota|  
|[3800 - RoutingServiceClosingClient](3800-routingserviceclosingclient.md)|Informações|O serviço de roteamento está fechando o cliente ' %1 '.|Roteamentoservices|  
|[3800 - RoutingServiceClosingClient](3800-routingserviceclosingclient.md)|Aviso|Falha no cliente ' %1 ' do serviço de roteamento.|Roteamentoservices|  
|[3802 - RoutingServiceCompletingOneWay](3802-routingservicecompletingoneway.md)|Informações|Uma mensagem de uma maneira do serviço de roteamento está sendo concluída.|Roteamentoservices|  
|[3803 - RoutingServiceProcessingFailure](3803-routingserviceprocessingfailure.md)|Erro do|O serviço de roteamento falhou ao processar uma mensagem no ponto de extremidade com o endereço ' %1 '.|Roteamentoservices|  
|[3804 - RoutingServiceCreatingClientForEndpoint](3804-routingservicecreatingclientforendpoint.md)|Informações|O serviço de roteamento está criando um cliente para o ponto de extremidade: ' %1 '.|Roteamentoservices|  
|[3805 - RoutingServiceDisplayConfig](3805-routingservicedisplayconfig.md)|Detalhado|O serviço de roteamento está configurado com RouteOnHeadersOnly: %1, SoapProcessingEnabled: %2, EnsureOrderedDispatch: %3.|Roteamentoservices|  
|[3807 - RoutingServiceCompletingTwoWay](3807-routingservicecompletingtwoway.md)|Informações|Uma mensagem de resposta de solicitação de serviço de roteamento está sendo concluída.|Roteamentoservices|  
|[3809 - RoutingServiceMessageRoutedToEndpoints](3809-routingservicemessageroutedtoendpoints.md)|Detalhado|A mensagem roteada do serviço de roteamento com ID: ' %1 ' para %2 listas de pontos de extremidade.|Roteamentoservices|  
|[3810 - RoutingServiceConfigurationApplied](3810-routingserviceconfigurationapplied.md)|Informações|Um novo RoutingConfiguration foi aplicado ao serviço de roteamento.|Roteamentoservices|  
|[3815 - RoutingServiceProcessingMessage](3815-routingserviceprocessingmessage.md)|Informações|O serviço de roteamento está processando uma mensagem com ID: ' %1 ', ação: ' %2 ', URL de entrada: ' %3 ' recebida na transação: %4.|Roteamentoservices|  
|[3816 - RoutingServiceTransmittingMessage](3816-routingservicetransmittingmessage.md)|Informações|O serviço de roteamento está transmitindo a mensagem com a ID: ' %1 ' [operação %2] para ' %3 '.|Roteamentoservices|  
|[3817 - RoutingServiceCommittingTransaction](3817-routingservicecommittingtransaction.md)|Informações|O serviço de roteamento está confirmando uma transação com ID: ' %1 '.|Roteamentoservices|  
|[3818 - RoutingServiceDuplexCallbackException](3818-routingserviceduplexcallbackexception.md)|Erro do|O componente de serviço de roteamento %1 encontrou uma exceção de retorno de chamada duplex.|Roteamentoservices|  
|[3819 - RoutingServiceMovedToBackup](3819-routingservicemovedtobackup.md)|Informações|A mensagem de serviço de roteamento com ID: ' %1 ' [operação %2] foi movida para o ponto de extremidade de backup ' %3 '.|Roteamentoservices|  
|[3820 - RoutingServiceCreatingTransaction](3820-routingservicecreatingtransaction.md)|Informações|O serviço de roteamento criou uma nova transação com a ID ' %1 ' para processar mensagem (ns).|Roteamentoservices|  
|[3821 - RoutingServiceCloseFailed](3821-routingserviceclosefailed.md)|Aviso|Falha do serviço de roteamento ao fechar o cliente de saída ' %1 '.|Roteamentoservices|  
|[3822 - RoutingServiceSendingResponse](3822-routingservicesendingresponse.md)|Informações|O serviço de roteamento está enviando uma mensagem de resposta com a ação ' %1 '.|Roteamentoservices|  
|[3823 - RoutingServiceSendingFaultResponse](3823-routingservicesendingfaultresponse.md)|Aviso|O serviço de roteamento está enviando de volta uma mensagem de resposta de falha com a ação ' %1 '.|Roteamentoservices|  
|[3824 - RoutingServiceCompletingReceiveContext](3824-routingservicecompletingreceivecontext.md)|Detalhado|O serviço de roteamento está chamando ReceiveContext. Complete para a mensagem com ID: ' %1 '.|Roteamentoservices|  
|[3825 - RoutingServiceAbandoningReceiveContext](3825-routingserviceabandoningreceivecontext.md)|Aviso|O serviço de roteamento está chamando ReceiveContext. Abandon para a mensagem com ID: ' %1 '.|Roteamentoservices|  
|[3826 - RoutingServiceUsingExistingTransaction](3826-routingserviceusingexistingtransaction.md)|Detalhado|O serviço de roteamento enviará mensagens usando a transação existente ' %1 '.|Roteamentoservices|  
|[3827 - RoutingServiceTransmitFailed](3827-routingservicetransmitfailed.md)|Aviso|O serviço de roteamento falhou ao enviar para ' %1 '.|Roteamentoservices|  
|[3828 - RoutingServiceFilterTableMatchStart](3828-routingservicefiltertablematchstart.md)|Informações|Início da correspondência de MessageFilterTable do serviço de roteamento.|Roteamentoservices|  
|[3829 - RoutingServiceFilterTableMatchStop](3829-routingservicefiltertablematchstop.md)|Informações|Serviço de roteamento MessageFilterTable correspondência de interrupção.|Roteamentoservices|  
|[3830 - RoutingServiceAbortingChannel](3830-routingserviceabortingchannel.md)|Detalhado|O serviço de roteamento está chamando Abort no canal: ' %1 '.|Roteamentoservices|  
|[3831 - RoutingServiceHandledException](3831-routingservicehandledexception.md)|Detalhado|O serviço de roteamento tratou uma exceção.|Roteamentoservices|  
|[3832 - RoutingServiceTransmitSucceeded](3832-routingservicetransmitsucceeded.md)|Informações|O serviço de roteamento transmitiu com êxito a mensagem com a ID: ' %1 [operação %2] para ' %3 '.|Roteamentoservices|  
|[4001 - TransportListenerSessionsReceived](4001-transportlistenersessionsreceived.md)|Detalhado|Sessão de ouvinte de transporte recebida com via ' %1 '|Ativaçãoservices|  
|[4002 - FailFastException](4002-failfastexception.md)|Crítico|FailFastexception.|Ativaçãoservices|  
|[4003 - ServiceStartPipeError](4003-servicestartpipeerror.md)|Erro do|Erro de pipe inicial do serviço.|Ativaçãoservices|  
|[4008 - DispatchSessionStart](4008-dispatchsessionstart.md)|Detalhado|Distribuição de sessão iniciada.|Ativaçãoservices|  
|[4008 - DispatchSessionStart](4008-dispatchsessionstart.md)|Aviso|A expedição de sessão para ' %1 ' falhou porque a fila de sessões pendentes está cheia com ' %2 ' itens pendentes.|Ativaçãoservices|  
|[4011 - MessageQueueRegisterStart](4011-messagequeueregisterstart.md)|Detalhado|Início do registro da fila de mensagens.|Ativaçãoservices|  
|[4012 - MessageQueueRegisterAbort](4012-messagequeueregisterabort.md)|Erro do|O registro da fila de mensagens foi anulado com o status: ' %1 ' para o URI: ' %2 '.|Ativaçãoservices|  
|[4013 - MessageQueueUnregisterSucceeded](4013-messagequeueunregistersucceeded.md)|Detalhado|O cancelamento do registro da fila de mensagens foi bem-sucedido para o URI: ' %1 '.|Ativaçãoservices|  
|[4014 - MessageQueueRegisterFailed](4014-messagequeueregisterfailed.md)|Erro do|Falha no registro da fila de mensagens para o URI: ' %1 ' com o status: ' %2 '.|Ativaçãoservices|  
|[4015 - MessageQueueRegisterCompleted](4015-messagequeueregistercompleted.md)|Informações|Registro da fila de mensagens concluído para o URI ' %1 '.|Ativaçãoservices|  
|[4016 - MessageQueueDuplicatedSocketError](4016-messagequeueduplicatedsocketerror.md)|Erro do|A fila de mensagens falhou ao duplicar o soquete.|Ativaçãoservices|  
|[4019 - MessageQueueDuplicatedSocketComplete](4019-messagequeueduplicatedsocketcomplete.md)|Detalhado|MessageQueueDuplicatedSocketComplete|Ativaçãoservices|  
|[4020 - TcpTransportListenerListeningStart](4020-tcptransportlistenerlisteningstart.md)|Detalhado|Ouvinte de transporte TCP começando a escutar no URI: ' %1 '.|Ativaçãoservices|  
|[4021 - TcpTransportListenerListeningStop](4021-tcptransportlistenerlisteningstop.md)|Detalhado|Ouvinte de transporte TCP escutando.|Ativaçãoservices|  
|[4022 - WebhostUnregisterProtocolFailed](4022-webhostunregisterprotocolfailed.md)|Erro do|Código de erro: %1|Ativaçãoservices|  
|[4023 - WasCloseAllListenerChannelInstancesCompleted](4023-wasclosealllistenerchannelinstancescompleted.md)|Informações|Estava fechando todas as instâncias de canal do ouvinte concluídas.|Ativaçãoservices|  
|[4024 - WasCloseAllListenerChannelInstancesFailed](4024-wasclosealllistenerchannelinstancesfailed.md)|Erro do|Código de erro: %1|Ativaçãoservices|  
|[4025 - OpenListenerChannelInstanceFailed](4025-openlistenerchannelinstancefailed.md)|Erro do|Código de erro: %1|Ativaçãoservices|  
|[4026 - WasConnected](4026-wasconnected.md)|Detalhado|ESTAVA conectado.|Ativaçãoservices|  
|[4027 - WasDisconnected](4027-wasdisconnected.md)|Detalhado|FOI desconectado.|Ativaçãoservices|  
|[4028 - PipeTransportListenerListeningStart](4028-pipetransportlistenerlisteningstart.md)|Detalhado|Início da escuta do ouvinte de transporte de pipe no URI: %1.|Ativaçãoservices|  
|[4029 - PipeTransportListenerListeningStop](4029-pipetransportlistenerlisteningstop.md)|Detalhado|Parada de escuta de ouvinte de transporte de pipe.|Ativaçãoservices|  
|[4030 - DispatchSessionSuccess](4030-dispatchsessionsuccess.md)|Informações|Distribuição de sessão bem-sucedida.|Ativaçãoservices|  
|[4031 - DispatchSessionFailed](4031-dispatchsessionfailed.md)|Erro do|Falha na expedição da sessão.|Ativaçãoservices|  
|[4032 - WasConnectionTimedout](4032-wasconnectiontimedout.md)|Crítico|A conexão WAS atingiu o tempo limite.|Ativaçãoservices|  
|[4033 - RoutingTableLookupStart](4033-routingtablelookupstart.md)|Detalhado|Pesquisa de tabela de roteamento iniciada.|Ativaçãoservices|  
|[4034 - RoutingTableLookupStop](4034-routingtablelookupstop.md)|Detalhado|Pesquisa de tabela de roteamento concluída.|Ativaçãoservices|  
|[4035 - PendingSessionQueueRatio](4035-pendingsessionqueueratio.md)|Detalhado|Taxa da fila de sessões pendentes: %1/%2|Quota|  
|[4600 - MessageLogEventSizeExceeded](4600-messagelogeventsizeexceeded.md)|Aviso|Não foi possível registrar a mensagem, pois ela excede o tamanho do evento ETW|WCFMessageLogging|  
|[4801 - DiscoveryClientInClientChannelFailedToClose](4801-discoveryclientinclientchannelfailedtoclose.md)|Aviso|O DiscoveryClient criado dentro de DiscoveryClientChannel falhou ao fechar e, portanto, foi anulado.|Descoberta|  
|[4802 - DiscoveryClientProtocolExceptionSuppressed](4802-discoveryclientprotocolexceptionsuppressed.md)|Informações|Uma ProtocolException foi suprimida ao fechar o DiscoveryClient. Isso pode ocorrer porque um DiscoveryService ainda está tentando enviar resposta para o DiscoveryClient.|Descoberta|  
|[4803 - DiscoveryClientReceivedMulticastSuppression](4803-discoveryclientreceivedmulticastsuppression.md)|Informações|O DiscoveryClient recebeu uma mensagem de supressão multicast de um DiscoveryProxy.|Descoberta|  
|[4804 - DiscoveryMessageReceivedAfterOperationCompleted](4804-discoverymessagereceivedafteroperationcompleted.md)|Informações|Uma mensagem %1 com messageId = ' %2 ' foi descartada pelo DiscoveryClient porque a operação %3 correspondente foi concluída.|Descoberta|  
|[4805 - DiscoveryMessageWithInvalidContent](4805-discoverymessagewithinvalidcontent.md)|Aviso|Uma mensagem %1 com messageId = ' %2 ' foi descartada porque tinha conteúdo inválido.|Descoberta|  
|[4806 - DiscoveryMessageWithInvalidRelatesToOrOperationCompleted](4806-discoverymessagewithinvalidrelatestooroperationcompleted.md)|Aviso|Uma mensagem %1 com messageId = ' %2 ' e relatestse = ' %3 ' foi descartada pelo DiscoveryClient porque a operação %4 correspondente foi concluída ou o valor de RelatesTo é inválido.|Descoberta|  
|[4807 - DiscoveryMessageWithInvalidReplyTo](4807-discoverymessagewithinvalidreplyto.md)|Aviso|Uma mensagem de solicitação de descoberta com messageId = ' %1 ' foi descartada porque tinha um endereço ReplyTo inválido.|Descoberta|  
|[4808 - DiscoveryMessageWithNoContent](4808-discoverymessagewithnocontent.md)|Aviso|Uma mensagem %1 foi descartada porque não tinha nenhum conteúdo.|Descoberta|  
|[4809 - DiscoveryMessageWithNullMessageId](4809-discoverymessagewithnullmessageid.md)|Aviso|Uma mensagem %1 foi descartada porque o cabeçalho da mensagem não continha a propriedade MessageId necessária.|Descoberta|  
|[4810 - DiscoveryMessageWithNullMessageSequence](4810-discoverymessagewithnullmessagesequence.md)|Aviso|Uma mensagem %1 com messageId = ' %2 ' foi descartada pelo DiscoveryClient porque ela não tinha a Propriedade DiscoveryMessageSequence.|Descoberta|  
|[4811 - DiscoveryMessageWithNullRelatesTo](4811-discoverymessagewithnullrelatesto.md)|Aviso|Uma mensagem %1 com messageId = ' %2 ' foi descartada pelo DiscoveryClient porque o cabeçalho da mensagem não continha a propriedade relatesta necessária.|Descoberta|  
|[4812 - DiscoveryMessageWithNullReplyTo](4812-discoverymessagewithnullreplyto.md)|Aviso|Uma mensagem de solicitação de descoberta com messageId = ' %1 ' foi descartada porque não tinha um endereço ReplyTo.|Descoberta|  
|[4813 - DuplicateDiscoveryMessage](4813-duplicatediscoverymessage.md)|Aviso|Uma mensagem %1 com messageId = ' %2 ' foi descartada porque ela era uma duplicata.|Descoberta|  
|[4814 - EndpointDiscoverabilityDisabled](4814-endpointdiscoverabilitydisabled.md)|Informações|A capacidade de descoberta do ponto de extremidade com EndpointAddress = ' %1 ' e ListenUri = ' %2 ' foi desabilitada.|Descoberta|  
|[4814 - EndpointDiscoverabilityDisabled](4814-endpointdiscoverabilitydisabled.md)|Informações|A capacidade de descoberta do ponto de extremidade com EndpointAddress = ' %1 ' e ListenUri = ' %2 ' foi habilitada.|Descoberta|  
|[4816 - FindInitiatedInDiscoveryClientChannel](4816-findinitiatedindiscoveryclientchannel.md)|Detalhado|Uma operação de localização foi iniciada no DiscoveryClientChannel para descobrir os pontos de extremidade.|Descoberta|  
|[4817 - InnerChannelCreationFailed](4817-innerchannelcreationfailed.md)|Aviso|Falha do DiscoveryClientChannel ao criar o canal com um ponto de extremidade descoberto com EndpointAddress = ' %1 ' e via = ' %2 '. Agora, o DiscoveryClientChannel tentará usar o próximo ponto de extremidade descoberto disponível.|Descoberta|  
|[4818 - InnerChannelOpenFailed](4818-innerchannelopenfailed.md)|Aviso|Falha do DiscoveryClientChannel ao abrir o canal com um ponto de extremidade descoberto com EndpointAddress = ' %1 ' e via = ' %2 '. Agora, o DiscoveryClientChannel tentará usar o próximo ponto de extremidade descoberto disponível.|Descoberta|  
|[4819 - InnerChannelOpenSucceeded](4819-innerchannelopensucceeded.md)|Informações|O DiscoveryClientChannel descobriu com êxito um ponto de extremidade e abriu o canal usando-o. O cliente está conectado a um serviço usando EndpointAddress = ' %1 ' e via = ' %2 '.|Descoberta|  
|[4820 - SynchronizationContextReset](4820-synchronizationcontextreset.md)|Informações|O SynchronizationContext foi redefinido para seu valor original de %1 pelo DiscoveryClientChannel.|Descoberta|  
|[4821 - SynchronizationContextSetToNull](4821-synchronizationcontextsettonull.md)|Informações|O SynchronizationContext foi definido como nulo pelo DiscoveryClientChannel antes de iniciar a operação Find.|Descoberta|  
|[5001 - DCSerializeWithSurrogateStart](5001-dcserializewithsurrogatestart.md)|Detalhado|Início da serialização DataContract de %1 com substitutos.|Serialização|  
|[5002 - DCSerializeWithSurrogateStop](5002-dcserializewithsurrogatestop.md)|Detalhado|Parada de serialização DataContract com substitutos.|Serialização|  
|[5003 - DCDeserializeWithSurrogateStart](5003-dcdeserializewithsurrogatestart.md)|Detalhado|Início da desserialização DataContract de %1 com substitutos.|Serialização|  
|[5004 - DCDeserializeWithSurrogateStop](5004-dcdeserializewithsurrogatestop.md)|Detalhado|Parada de desserialização DataContract com substitutos.|Serialização|  
|[5005 - ImportKnownTypesStart](5005-importknowntypesstart.md)|Detalhado|ImportKnownTypes iniciar.|Serialização|  
|[5006 - ImportKnownTypesStop](5006-importknowntypesstop.md)|Detalhado|ImportKnownTypes parar.|Serialização|  
|[5007 - DCResolverResolve](5007-dcresolverresolve.md)|Detalhado|Início da resolução do resolvedor DataContract %1.|Serialização|  
|[5008 - DCGenWriterStart](5008-dcgenwriterstart.md)|Detalhado|Início do gravador DataContract %1 para %2.|Serialização|  
|[5009 - DCGenWriterStop](5009-dcgenwriterstop.md)|Detalhado|Parada do gravador de geração DataContract.|Serialização|  
|[5010 - DCGenReaderStart](5010-dcgenreaderstart.md)|Detalhado|Início do leitor de geração DataContract %1 para %2.|Serialização|  
|[5011 - DCGenReaderStop](5011-dcgenreaderstop.md)|Detalhado|Parada de geração DataContract.|Serialização|  
|[5012 - DCJsonGenReaderStart](5012-dcjsongenreaderstart.md)|Detalhado|Início do leitor de geração de JSON %1 para %2.|Serialização|  
|[5013 - DCJsonGenReaderStop](5013-dcjsongenreaderstop.md)|Detalhado|Parada de geração de leitor JSON.|Serialização|  
|[5014 - DCJsonGenWriterStart](5014-dcjsongenwriterstart.md)|Detalhado|Início do gravador de geração JSON %1 para %2.|Serialização|  
|[5015 - DCJsonGenWriterStop](5015-dcjsongenwriterstop.md)|Detalhado|Parada de gravador de geração JSON.|Serialização|  
|[5016 - GenXmlSerializableStart](5016-genxmlserializablestart.md)|Detalhado|Início da geração de XML serializável para ' %1 '.|Serialização|  
|[5017 - GenXmlSerializableStop](5017-genxmlserializablestop.md)|Detalhado|Parada de geração de XML serializável.|Serialização|  
|[5203 - JsonMessageDecodingStart](5203-jsonmessagedecodingstart.md)|Detalhado|JsonMessageEncoder iniciou a decodificação da mensagem.|Canal|  
|[5204 - JsonMessageEncodingStart](5204-jsonmessageencodingstart.md)|Detalhado|JsonMessageEncoder iniciou a codificação da mensagem.|Canal|  
|[5402 - TokenValidationStarted](5402-tokenvalidationstarted.md)|Detalhado|Validação de SecurityToken (tipo ' %1 ' e ID ' %2 ') iniciada.|Segurança|  
|[5403 - TokenValidationSuccess](5403-tokenvalidationsuccess.md)|Detalhado|Validação de SecurityToken (tipo ' %1 ' e ID ' %2 ') bem-sucedida.|Segurança|  
|[5404 - TokenValidationFailure](5404-tokenvalidationfailure.md)|Erro do|Falha na validação de SecurityToken (tipo ' %1 ' e ID ' %2 '). %3|Segurança|  
|[5405 - GetIssuerNameSuccess](5405-getissuernamesuccess.md)|Detalhado|Recuperação do nome do emissor: %1 de tokenid: %2 com êxito.|Segurança|  
|[5406 - GetIssuerNameFailure](5406-getissuernamefailure.md)|Erro do|Falha na recuperação do nome do emissor de tokenid: %1.|Segurança|  
|[5600 - FederationMessageProcessingStarted](5600-federationmessageprocessingstarted.md)|Detalhado|Processamento de mensagem de Federação iniciado.|Segurança|  
|[5601 - FederationMessageProcessingSuccess](5601-federationmessageprocessingsuccess.md)|Detalhado|Processamento de mensagem de Federação bem-sucedido.|Segurança|  
|[5602 - FederationMessageCreationStarted](5602-federationmessagecreationstarted.md)|Detalhado|Criação de mensagem de Federação a partir do formulário de postagem iniciada.|Segurança|  
|[5603 - FederationMessageCreationSuccess](5603-federationmessagecreationsuccess.md)|Detalhado|A criação da mensagem de Federação da postagem do formulário foi bem-sucedida.|Segurança|  
|[5604 - SessionCookieReadingStarted](5604-sessioncookiereadingstarted.md)|Detalhado|Leitura do token de sessão do cookie de sessão iniciada.|Segurança|  
|[5605 - SessionCookieReadingSuccess](5605-sessioncookiereadingsuccess.md)|Detalhado|Leitura do token de sessão do cookie de sessão bem-sucedida.|Segurança|  
|[5606 - PrincipalSettingFromSessionTokenStarted](5606-principalsettingfromsessiontokenstarted.md)|Detalhado|Configuração da entidade de segurança do token de sessão iniciada.|Segurança|  
|[5607 - PrincipalSettingFromSessionTokenSuccess](5607-principalsettingfromsessiontokensuccess.md)|Detalhado|Configuração da entidade de segurança do token de sessão bem-sucedida.|Segurança|  
|[57393 - AppDomainUnload](57393-appdomainunload.md)|Informações|Descarregamento de AppDomain. AppDomain. FriendlyName %1, ProcessName %2, ProcessId %3.|Infraestrutura|  
|[57394 - HandledException](57394-handledexception.md)|Informações|Tratando uma exceção.|Infraestrutura|  
|[57395 - ShipAssertExceptionMessage](57395-shipassertexceptionmessage.md)|Erro do|Ocorreu uma falha inesperada. Os aplicativos não devem tentar tratar esse erro. Para fins de diagnóstico, esta mensagem em inglês está associada à falha: %1.|Infraestrutura|  
|[57396 - ThrowingException](57396-throwingexception.md)|Aviso|Gerando uma exceção. Origem %1.|Infraestrutura|  
|[57397 - UnhandledException](57397-unhandledexception.md)|Crítico|Exceção sem tratamento.|Infraestrutura|  
|[57399 - TraceCodeEventLogCritical](57399-tracecodeeventlogcritical.md)|Crítico|Gravado no log de eventos.|Infraestrutura|  
|[57400 - TraceCodeEventLogError](57400-tracecodeeventlogerror.md)|Erro do|Gravado no log de eventos.|Infraestrutura|  
|[57401 - TraceCodeEventLogInfo](57401-tracecodeeventloginfo.md)|Informações|Gravado no log de eventos.|Infraestrutura|  
|[57402 - TraceCodeEventLogVerbose](57402-tracecodeeventlogverbose.md)|Detalhado|Gravado no log de eventos.|Infraestrutura|  
|[57403 - TraceCodeEventLogWarning](57403-tracecodeeventlogwarning.md)|Aviso|Gravado no log de eventos.|Infraestrutura|  
|[57404 - HandledExceptionWarning](57404-handledexceptionwarning.md)|Aviso|Tratando uma exceção.|Infraestrutura|  
|[62326 - HttpHandlerPickedForUrl](62326-httphandlerpickedforurl.md)|Informações|A URL ' %1 ' hospeda o documento XAML com o tipo de elemento raiz ' %2 '. O tipo de manipulador HTTP ' %3 ' foi escolhido para atender a todas as solicitações feitas a esta URL.|WebHost|
