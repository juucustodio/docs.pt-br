---
description: 'Saiba mais sobre: referência de eventos de rastreamento'
title: Referência de eventos de rastreamento
ms.date: 03/30/2017
ms.assetid: c1c1ee87-f80a-449b-acd0-50d81eef116e
ms.openlocfilehash: 64df938dc7e37ebc8b3da8f10939bebe1e638be1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755181"
---
# <a name="tracking-events-reference"></a>Referência de eventos de rastreamento

Durante a execução um fluxo de trabalho aumenta de [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] que acompanham eventos como se move por várias etapas no tempo de vida. O host pode assinar esses eventos e ter atualizado no status de progresso de fluxo de trabalho durante seu ciclo de vida. Os eventos de rastreamento gerados são discutidos nesta seção.  
  
## <a name="event-reference"></a>Referência de eventos  
  
|ID do evento|Evento em nível|Mensagem de evento|Palavras-chave|  
|--------------|-----------------|-------------------|--------------|  
|[100 - WorkflowInstanceRecord](100-workflowinstancerecord.md)|Informações|TrackRecord= WorkflowInstanceRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, estado = %5, anotações = %6 ProfileName, %7 =|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[101 - WorkflowInstanceUnhandledExceptionRecord](101-workflowinstanceunhandledexceptionrecord.md)|Erro do|TrackRecord = WorkflowInstanceUnhandledExceptionRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, SourceName = %5, SourceId = %6, SourceInstanceId =, %7 SourceTypeName=%8, Exception=%9, Annotations= %10, ProfileName = %11|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[102 - WorkflowInstanceAbortedRecord](102-workflowinstanceabortedrecord.md)|Aviso|TrackRecord = WorkflowInstanceAbortedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razão = %5, anotações = %6 ProfileName, %7 =|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[103 - ActivityStateRecord](103-activitystaterecord.md)|Informações|TrackRecord = ActivityStateRecord, InstanceID = %1, RecordNumber=%2, EventTime=%3, estado = %4, Name=%5, ActivityId=%6, ActivityInstanceId=%7, ActivityTypeName=%8, Arguments=%9, Variables=%10, Annotations=%11, ProfileName = %12|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[104 - ActivityScheduledRecord](104-activityscheduledrecord.md)|Informações|TrackRecord = ActivityScheduledRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, nome = %4, ActivityId = %5, ActivityInstanceId = %6, ActivityTypeName =, %7 ChildActivityName =, %8 ChildActivityId = %9, ChildActivityInstanceId = %10, ChildActivityTypeName =%11, Annotations=%12, ProfileName = %13|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[105 - FaultPropagationRecord](105-faultpropagationrecord.md)|Aviso|TrackRecord = FaultPropagationRecord, InstanceID=%1, RecordNumber=%2, EventTime=%3, FaultSourceActivityName=%4, FaultSourceActivityId=%5, FaultSourceActivityInstanceId=%6, FaultSourceActivityTypeName=%7, FaultHandlerActivityName=%8, FaultHandlerActivityId = %9, FaultHandlerActivityInstanceId =%10, FaultHandlerActivityTypeName=%11, Fault=%12, IsFaultSource=%13, Annotations=%14, ProfileName = %15|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[106 - CancelRequestRecord](106-cancelrequestrecord.md)|Informações|TrackRecord = CancelRequestedRecord, InstanceID=%1, RecordNumber=%2, EventTime=%3, Name=%4, ActivityId=%5, ActivityInstanceId=%6, ActivityTypeName =, %7 ChildActivityName =, %8 ChildActivityId = %9, ChildActivityInstanceId = %10, ChildActivityTypeName =%11, Annotations=%12, ProfileName = %13|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[107 -- BookmarkResumptionRecord](107-bookmarkresumptionrecord.md)|Informações|TrackRecord = BookmarkResumptionRecord, InstanceID=%1, RecordNumber=%2, EventTime=%3, Name=%4, SubInstanceID=%5, OwnerActivityName=%6, OwnerActivityId =%7, OwnerActivityInstanceId=%8, OwnerActivityTypeName=%9, Annotations=%10, ProfileName = %11|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[108 - CustomTrackingRecordInfo](108-customtrackingrecordinfo.md)|Informações|TrackRecord = CustomTrackingRecord, InstanceID = %1, RecordNumber=%2, EventTime=%3, Name=%4, ActivityName=%5, ActivityId=%6, ActivityInstanceId=%7, ActivityTypeName=%8, Data=%9, Annotations=%10, ProfileName = %11|UserEvents, EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[110 - CustomTrackingRecordWarning](110-customtrackingrecordwarning.md)|Aviso|TrackRecord = CustomTrackingRecord, InstanceID = %1, RecordNumber=%2, EventTime=%3, Name=%4, ActivityName=%5, ActivityId=%6, ActivityInstanceId=%7, ActivityTypeName=%8, Data=%9, Annotations=%10, ProfileName = %11|UserEvents, EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[111 - CustomTrackingRecordError](111-customtrackingrecorderror.md)|Erro do|TrackRecord = CustomTrackingRecord, InstanceID = %1, RecordNumber=%2, EventTime=%3, Name=%4, ActivityName=%5, ActivityId=%6, ActivityInstanceId=%7, ActivityTypeName=%8, Data=%9, Annotations=%10, ProfileName = %11|UserEvents, EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[112 - WorkflowInstanceSuspendedRecord](112-workflowinstancesuspendedrecord.md)|Informações|TrackRecord = WorkflowInstanceSuspendedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razão = %5, anotações = %6 ProfileName, %7 =|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[113 - WorkflowInstanceTerminatedRecord](113-workflowinstanceterminatedrecord.md)|Erro do|TrackRecord = WorkflowInstanceTerminatedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razão = %5, anotações = %6 ProfileName, %7 =|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|[114 - WorkflowInstanceRecordWithId](114-workflowinstancerecordwithid.md)|Informações|TrackRecord= WorkflowInstanceRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, estado = %5, anotações = %6 ProfileName, =, %7 WorkflowDefinitionIdentity = %8|HealthMonitoring, WFTracking|  
|[115 - WorkflowInstanceAbortedRecordWithId](115-workflowinstanceabortedrecordwithid.md)|Aviso|TrackRecord = WorkflowInstanceAbortedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razão = %5, anotações = %6 ProfileName, =, %7 WorkflowDefinitionIdentity = %8|HealthMonitoring, WFTracking|  
|[116 - WorkflowInstanceSuspendedRecordWithId](116-workflowinstancesuspendedrecordwithid.md)|Informações|TrackRecord = WorkflowInstanceSuspendedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razão = %5, anotações = %6 ProfileName, =, %7 WorkflowDefinitionIdentity = %8|HealthMonitoring, WFTracking|  
|[117 - WorkflowInstanceTerminatedRecordWithId](117-workflowinstanceterminatedrecordwithid.md)|Erro do|TrackRecord = WorkflowInstanceTerminatedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razão = %5, anotações = %6 ProfileName, =, %7 WorkflowDefinitionIdentity = %8|HealthMonitoring, WFTracking|  
|[118 - WorkflowInstanceUnhandledExceptionRecordWithId](118-workflowinstanceunhandledexceptionrecordwithid.md)|Erro do|TrackRecord = WorkflowInstanceUnhandledExceptionRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, SourceName = %5, SourceId = %6, SourceInstanceId =, %7 SourceTypeName=%8, Exception=%9, Annotations= %10, ProfileName = %11, WorkflowDefinitionIdentity = %12|HealthMonitoring, WFTrackingHealthMonitoring, WFTracking|  
|[119 - WorkflowInstanceUpdatedRecord](119-workflowinstanceupdatedrecord.md)|Informações|TrackRecord= WorkflowInstanceUpdatedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, estado = %5, OriginalDefinitionIdentity = %6, UpdatedDefinitionIdentity = %7, anotações =, %8 ProfileName = %9|HealthMonitoring, WFTracking|  
|[225 - TraceCorrelationKeys](225-tracecorrelationkeys.md)|Informações|Chave calculada “%1 " de correlação usando o %2 " dos valores no escopo pai “%3 ".|Solução de problemas WFServices|  
|[440 - StartSignpostEvent1](440-startsignpostevent.md)|Informações|Limite de atividade.|Solução de problemas WFServices|  
|[441- StopSignpostEvent1](441-stopsignpostevent.md)|Informações|Limite de atividade.|Solução de problemas WFServices|  
|[1001 - WorkflowApplicationCompleted](1001-workflowapplicationcompleted.md)|Informações|Identificação de WorkflowInstance: “%1 " terminou no estado fechado.|WFRuntime|  
|[1002 - WorkflowApplicationTerminated](1002-workflowapplicationterminated.md)|Informações|Identificação de WorkflowApplication: “%1 " foi encerrado. Foi concluído em estado Faulted (com falha) com uma exceção.|WFRuntime|  
|[1003 - WorkflowInstanceCanceled](1003-workflowinstancecanceled.md)|Informações|Identificação de WorkflowInstance: “%1 " terminou no estado cancelado.|WFRuntime|  
|[1004 - WorkflowInstanceAborted](1004-workflowinstanceaborted.md)|Informações|Identificação de WorkflowInstance: “%1 " foi anuladas com uma exceção.|WFRuntime|  
|[1005 - WorkflowApplicationIdled](1005-workflowapplicationidled.md)|Informações|Identificação de WorkflowApplication: “%1 " foi ociosa.|WFRuntime|  
|[1006 - WorkflowApplicationUnhandledException](1006-workflowapplicationunhandledexception.md)|Erro do|WorkflowInstance ID: ' %1 ' encontrou uma exceção sem tratamento.  A exceção foi originada da atividade ' %2 ', DisplayName: ' %3 '.  A seguinte ação será executada: %4.|WFRuntime|  
|[1007 - WorkflowApplicationPersisted](1007-workflowapplicationpersisted.md)|Informações|Identificação de WorkflowApplication: “%1 " foi persistente.|WFRuntime|  
|[1008 - WorkflowApplicationUnloaded](1008-workflowapplicationunloaded.md)|Informações|Identificação de WorkflowInstance: “%1" foi descarregado.|WFRuntime|  
|[1009 - ActivityScheduled](1009-activityscheduled.md)|Informações|Atividade pai “%1", DisplayName: “%2", InstanceId: “%3" agendaram a atividade filho “%4", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1010 - ActivityCompleted](1010-activitycompleted.md)|Informações|Atividade pai “%1", DisplayName: “%2", InstanceId: “%3" agendaram a atividade filho “%4", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1011 - ScheduleExecuteActivityWorkItem](1011-scheduleexecuteactivityworkitem.md)|Detalhado|Um ExecuteActivityWorkItem foi agendada para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1012 - StartExecuteActivityWorkItem](1012-startexecuteactivityworkitem.md)|Detalhado|Iniciar a execução de um ExecuteActivityWorkItem para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1013 - CompleteExecuteActivityWorkItem](1013-completeexecuteactivityworkitem.md)|Detalhado|Um ExecuteActivityWorkItem concluiu para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1014 - ScheduleCompletionWorkItem](1014-schedulecompletionworkitem.md)|Detalhado|Um CompletionWorkItem foi agendado para a atividade pai ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  Atividade counting “%4 ", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1015 - StartCompletionWorkItem](1015-startcompletionworkitem.md)|Detalhado|Iniciar a execução de um CompletionWorkItem para atividades pai “%1 ", DisplayName: “%2", InstanceId: “%3". Atividade counting “%4 ", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1016 - CompleteCompletionWorkItem](1016-completecompletionworkitem.md)|Detalhado|Um CompletionWorkItem concluiu para atividades pai “%1 ", DisplayName: “%2", InstanceId: “%3". Atividade counting “%4 ", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1017 - ScheduleCancelActivityWorkItem](1017-schedulecancelactivityworkitem.md)|Detalhado|Um CancelActivityWorkItem foi agendada para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1018 - StartCancelActivityWorkItem](1018-startcancelactivityworkitem.md)|Detalhado|Iniciar a execução de um CancelActivityWorkItem para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1019 - CompleteCancelActivityWorkItem](1019-completecancelactivityworkitem.md)|Detalhado|Um CancelActivityWorkItem concluiu para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1020 - CreateBookmark](1020-createbookmark.md)|Detalhado|Um indicador foi criado para a atividade ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  BookmarkName: %4, BookmarkScope: %5.|WFRuntime|  
|[1021 - ScheduleBookmarkWorkItem](1021-schedulebookmarkworkitem.md)|Detalhado|Um BookmarkWorkItem foi agendado para a atividade ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  BookmarkName: %4, BookmarkScope: %5.|WFRuntime|  
|[1022 - StartBookmarkWorkItem](1022-startbookmarkworkitem.md)|Detalhado|Iniciando a execução de um BookmarkWorkItem para a atividade ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  BookmarkName: %4, BookmarkScope: %5.|WFRuntime|  
|[1023 - CompleteBookmarkWorkItem](1023-completebookmarkworkitem.md)|Detalhado|Um BookmarkWorkItem concluiu para atividades “%1 ", DisplayName: “%2", InstanceId: “%3". BookmarkName: %4, BookmarkScope: %5.|WFRuntime|  
|[1024 - CreateBookmarkScope](1024-createbookmarkscope.md)|Detalhado|Um BookmarkScope foi criado: %1.|WFRuntime|  
|[1025 - BookmarkScopeInitialized](1025-bookmarkscopeinitialized.md)|Detalhado|O BookmarkScope que tinha TemporaryId: “%1 " foi inicializado com ID: “%2".|WFRuntime|  
|[1026 - ScheduleTransactionContextWorkItem](1026-scheduletransactioncontextworkitem.md)|Detalhado|Um TransactionContextWorkItem foi agendada para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1027 - StartTransactionContextWorkItem](1027-starttransactioncontextworkitem.md)|Detalhado|Iniciar a execução de um TransactionContextWorkItem para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1028 - CompleteTransactionContextWorkItem](1028-completetransactioncontextworkitem.md)|Detalhado|Um TransactionContextWorkItem concluiu para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1029 - ScheduleFaultWorkItem](1029-schedulefaultworkitem.md)|Detalhado|Um FaultWorkItem foi agendado para a atividade ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  A exceção é propagada de atividade “%4 ", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1030 - StartFaultWorkItem](1030-startfaultworkitem.md)|Detalhado|Iniciando a execução de um FaultWorkItem para a atividade ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  A exceção é propagada de atividade “%4 ", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1031 - CompleteFaultWorkItem](1031-completefaultworkitem.md)|Detalhado|Um FaultWorkItem concluiu para atividades “%1 ", DisplayName: “%2", InstanceId: “%3". A exceção é propagada de atividade “%4 ", DisplayName: “%5", InstanceId: “%6".|WFRuntime|  
|[1032 - ScheduleRuntimeWorkItem](1032-scheduleruntimeworkitem.md)|Detalhado|Um item de trabalho de runtime foi agendada para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1033 - StartRuntimeWorkItem](1033-startruntimeworkitem.md)|Detalhado|Iniciar a execução de um item de trabalho de runtime para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1034 - CompleteRuntimeWorkItem](1034-completeruntimeworkitem.md)|Detalhado|Um item de trabalho de runtime concluiu para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".|WFRuntime|  
|[1035 - RuntimeTransactionSet](1035-runtimetransactionset.md)|Detalhado|A transação de tempo de execução foi definida pela atividade ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  Execução isolada para a atividade ' %4 ', DisplayName: ' %5 ', InstanceId: ' %6 '.|WFRuntime|  
|[1036 - RuntimeTransactionCompletionRequested](1036-runtimetransactioncompletionrequested.md)|Detalhado|Atividade “%1", DisplayName: “%2", InstanceId: “%3 " agendaram a conclusão de transação de runtime.|WFRuntime|  
|[1037 - RuntimeTransactionComplete](1037-runtimetransactioncomplete.md)|Detalhado|A transação de runtime terminou com o estado “%1 ".|WFRuntime|  
|[1038 - EnterNoPersistBlock](1038-enternopersistblock.md)|Detalhado|Entrando em um bloco sem persistência.|WFRuntime|  
|[1039 - ExitNoPersistBlock](1039-exitnopersistblock.md)|Detalhado|Saindo de um bloco sem persistência.|WFRuntime|  
|[1040 - InArgumentBound](1040-inargumentbound.md)|Detalhado|O argumento “%1 " na atividade “%2 ", DisplayName: “%3", InstanceId: “%4" foram associados com valor: %5.|WFActivities|  
|[1041 - WorkflowApplicationPersistableIdle](1041-workflowapplicationpersistableidle.md)|Informações|WorkflowApplication ID: ' %1 ' está ociosa e persistente.  A seguinte ação será executada: %2.|WFRuntime|  
|[1101 - WorkflowActivityStart](1101-workflowactivitystart.md)|Informações|Identificação de WorkflowInstance: “%1" atividade de E2E|WFRuntime|  
|[1102 - WorkflowActivityStop](1102-workflowactivitystop.md)|Informações|Identificação de WorkflowInstance: “%1" atividade de E2E|WFRuntime|  
|[1103 - WorkflowActivitySuspend](1103-workflowactivitysuspend.md)|Informações|Identificação de WorkflowInstance: “%1" atividade de E2E|WFRuntime|  
|[1104 - WorkflowActivityResume](1104-workflowactivityresume.md)|Informações|Identificação de WorkflowInstance: “%1" atividade de E2E|WFRuntime|  
|[1124 - InvokeMethodIsStatic](1124-invokemethodisstatic.md)|Informações|InvokeMethod “%1" - o método é estático.|WFRuntime|  
|[1125 - InvokeMethodIsNotStatic](1125-invokemethodisnotstatic.md)|Informações|InvokeMethod “%1" - o método não é estático.|WFRuntime|  
|[1126 - InvokedMethodThrewException](1126-invokedmethodthrewexception.md)|Informações|Uma exceção foi lançada no método chamado pela atividade “%1 ". %2|WFRuntime|  
|[1131 - InvokeMethodUseAsyncPattern](1131-invokemethoduseasyncpattern.md)|Informações|InvokeMethod “%1 " - o método utiliza o padrão assíncrono de “%2 " e “%3 ".|WFRuntime|  
|[1132 - InvokeMethodDoesNotUseAsyncPattern](1132-invokemethoddoesnotuseasyncpattern.md)|Informações|InvokeMethod “%1" - o método não usa o padrão assíncrono.|WFRuntime|  
|[1140 - FlowchartStart](1140-flowchartstart.md)|Informações|Fluxograma “%1 " - Início foi agendada.|WFActivities|  
|[1141 - FlowchartEmpty](1141-flowchartempty.md)|Aviso|O fluxograma “%1" - foi executado sem nós. Uma exceção foi lançada no método chamado pela atividade “%1 ". %2|WFActivities|  
|[1143 - FlowchartNextNull](1143-flowchartnextnull.md)|Informações|Fluxograma “%1 " /FlowStep - o nó seguir é nulo. A execução do fluxograma será finalizada.|WFActivities|  
|[1146 - FlowchartSwitchCase](1146-flowchartswitchcase.md)|Informações|Fluxograma “%1" /FlowSwitch - os casos “%2" foram selecionados.|WFActivities|  
|[1147 - FlowchartSwitchDefault](1147-flowchartswitchdefault.md)|Informações|Fluxograma “%1 " /FlowSwitch - os casos padrão foram selecionados.|WFActivities|  
|[1148 - FlowchartSwitchCaseNotFound](1148-flowchartswitchcasenotfound.md)|Informações|O fluxograma “%1 " /FlowSwitch - pôde localizar ou uma atividade dos casos ou casos padrão que correspondem ao resultado da expressão. A execução do fluxograma será finalizada.|WFActivities|  
|[1150 - CompensationState](1150-compensationstate.md)|Informações|CompensableActivity “%1 " está em “%2 " estado.|WFActivities|  
|[1223 - SwitchCaseNotFound](1223-switchcasenotfound.md)|Informações|A atividade “%1 " de opção não pôde encontrar uma atividade dos casos que corresponde ao resultado da expressão.|WFActivities|  
|[1449 - WfMessageReceived](1449-wfmessagereceived.md)|Informações|Mensagem recebida pelo fluxo de trabalho|WFServices|  
|[1450 - WfMessageSent](1450-wfmessagesent.md)|Informações|Mensagem enviada do fluxo de trabalho|WFServices|  
|[2021 - ExecuteWorkItemStart](2021-executeworkitemstart.md)|Detalhado|Executar início do item de trabalho|WFRuntime|  
|[2022 - ExecuteWorkItemStop](2022-executeworkitemstop.md)|Detalhado|Executar parada do item de trabalho|WFRuntime|  
|[2023 - SendMessageChannelCacheMiss](2023-sendmessagechannelcachemiss.md)|Detalhado|Erro de SendMessageChannelCache|WFRuntime|  
|[2024 - InternalCacheMetadataStart](2024-internalcachemetadatastart.md)|Detalhado|InternalCacheMetadata começou a atividade “%1 ".|WFRuntime|  
|[2025 - InternalCacheMetadataStop](2025-internalcachemetadatastop.md)|Detalhado|InternalCacheMetadata ter parado na atividade “%1 ".|WFRuntime|  
|[2026 - CompileVbExpressionStart](2026-compilevbexpressionstart.md)|Detalhado|Expressão “%1 " VB de compilação|WFRuntime|  
|[2027 - CacheRootMetadataStart](2027-cacherootmetadatastart.md)|Detalhado|CacheRootMetadata começou a atividade “%1 "|WFRuntime|  
|[2028 - CacheRootMetadataStop](2028-cacherootmetadatastop.md)|Detalhado|CacheRootMetadata ter parado na atividade %1.|WFRuntime|  
|[2029 - CompileVbExpressionStop](2029-compilevbexpressionstop.md)|Detalhado|Compilação da expressão do VB concluída.|WFRuntime|  
|[2576 - TryCatchExceptionFromTry](2576-trycatchexceptionfromtry.md)|Informações|A atividade “%1 " de TryCatch capturou uma exceção “%2 ".|WFActivities|  
|[2577 - TryCatchExceptionDuringCancelation](2577-trycatchexceptionduringcancelation.md)|Aviso|Uma atividade filho da atividade “%1 " de TryCatch apresentou uma exceção durante o cancelar.|WFActivities|  
|[2578 - TryCatchExceptionFromCatchOrFinally](2578-trycatchexceptionfromcatchorfinally.md)|Aviso|Uma captura ou finalmente a atividade que está associada com a atividade “%1 " de TryCatch apresentou uma exceção.|WFActivities|  
|[3501 - InferredContractDescription](3501-inferredcontractdescription.md)|Informações|ContractDescription com Name='%1 e Namespace='%2 foi inferido de WorkflowService.|WFServices|  
|[3502 - InferredOperationDescription](3502-inferredoperationdescription.md)|Informações|OperationDescription com o Name='%1 no contrato “%2 " foi inferido de WorkflowService. IsOneWay=%3.|WFServices|  
|[3503 - DuplicateCorrelationQuery](3503-duplicatecorrelationquery.md)|Aviso|Um CorrelationQuery duplicado foi encontrado com Where='%1. Essa consulta duplicada não será usada no cálculo de correlação.|WFServices|  
|[3507 - ServiceEndpointAdded](3507-serviceendpointadded.md)|Informações|Um ponto final de serviço foi adicionado para o endereço “%1 ", associando “%2 ", e reduz “%3 ".|WFServices|  
|[3508 - TrackingProfileNotFound](3508-trackingprofilenotfound.md)|Detalhado|TrackingProfile “%1 " para o ActivityDefinitionId “%2 " não encontrado. O TrackingProfile não é encontrado no arquivo de configuração ou a ActivityDefinitionId não é correspondente.|WFServices|  
|[3550 - BufferOutOfOrderMessageNoInstance](3550-bufferoutofordermessagenoinstance.md)|Informações|A operação “%1 " não pode ser executada no momento. Outra tentativa será feita quando a instância de serviço estiver pronta para processar esse operação específica.|WFServices|  
|[3551 - BufferOutOfOrderMessageNoBookmark](3551-bufferoutofordermessagenobookmark.md)|Informações|A operação “%2 " na instância “%1 " do serviço não pode ser executada no momento. Outra tentativa será feita quando a instância de serviço estiver pronta para processar esse operação específica.|WFServices|  
|[3552 - MaxPendingMessagesPerChannelExceeded](3552-maxpendingmessagesperchannelexceeded.md)|Aviso|O regulador de pressão “MaxPendingMessagesPerChannel” limite de “%1 " foi atingido. Para aumentar esse limite, ajuste a propriedade MaxPendingMessagesPerChannel no BufferedReceiveServiceBehavior.|Cota WFServices|  
|[3557 - TransactedReceiveScopeEndCommitFailed](3557-transactedreceivescopeendcommitfailed.md)|Informações|A chamada a EndCommit no CommittableTransaction com ID = “%1 " apresentou um TransactionException com a seguinte mensagem: “%2".|WFServices|  
|[4201 - EndSqlCommandExecute](4201-endsqlcommandexecute.md)|Detalhado|Execução do comando SQL de extremidade: %1|WFInstanceStore|  
|[4202 - StartSqlCommandExecute](4202-startsqlcommandexecute.md)|Detalhado|Iniciar a execução do comando SQL: %1|WFInstanceStore|  
|[4203 - RenewLockSystemError](4203-renewlocksystemerror.md)|Erro do|Falha em estender a validade do bloqueio; a validade do bloqueio já terminou ou o proprietário do bloqueio foi excluído. Anulando SqlWorkflowInstanceStore.|WFInstanceStore|  
|[4205 - FoundProcessingError](4205-foundprocessingerror.md)|Erro do|Comando falhou: %1|WFInstanceStore|  
|[4206 - UnlockInstanceException](4206-unlockinstanceexception.md)|Erro do|Exceção encontrada %1 ao tentar desbloquear a instância.|WFInstanceStore|  
|[4207 - MaximumRetriesExceededForSqlCommand](4207-maximumretriesexceededforsqlcommand.md)|Informações|Houve uma desistência de tentar um comando SQL como o número máximo de novas tentativas.|Cota WFInstanceStore|  
|[4208 - RetryingSqlCommandDueToSqlError](4208-retryingsqlcommandduetosqlerror.md)|Informações|Experimentando de novo um comando SQL por causa do erro número %1. SQL.|WFInstanceStore|  
|[4209 - TimeoutOpeningSqlConnection](4209-timeoutopeningsqlconnection.md)|Erro do|O tempo limite está tentando abrir uma conexão de SQL. A operação não concluiu dentro do tempo limite distribuído de %1. O tempo determinado para essa operação pode ter sido uma parte de um tempo limite maior.|WFInstanceStore|  
|[4210 - SqlExceptionCaught](4210-sqlexceptioncaught.md)|Aviso|Mensagem capturada %2 de %1. número de exceção SQL.|WFInstanceStore|  
|[4211 - QueuingSqlRetry](4211-queuingsqlretry.md)|Aviso|Nova tentativa SQL fila com atraso %1 milissegundos.|WFInstanceStore|  
|[4212 - LockRetryTimeout](4212-lockretrytimeout.md)|Aviso|Tempo limite ao tentar adquirir o bloqueio de instância.  A operação não concluiu dentro do tempo limite distribuído de %1. O tempo determinado para essa operação pode ter sido uma parte de um tempo limite maior.|WFInstanceStore|  
|[4213 - RunnableInstancesDetectionError](4213-runnableinstancesdetectionerror.md)|Erro do|Falha na detecção de instâncias executáveis devido à seguinte exceção|WFInstanceStore|  
|[4214 - InstanceLocksRecoveryError](4214-instancelocksrecoveryerror.md)|Erro do|Falha na recuperação dos bloqueios de instância devido à seguinte exceção|WFInstanceStore|  
|[39456 - TrackingRecordDropped](39456-trackingrecorddropped.md)|Aviso|O tamanho do registro %1 de rastreamento excede o máximo permitido pela sessão de ETW para o provedor %2|WFTracking|  
|[39457 - TrackingRecordRaised](39457-trackingrecordraised.md)|Informações|Controlando o registro %1 elevado a %2.|WFRuntime|  
|[39458 - TrackingRecordTruncated](39458-trackingrecordtruncated.md)|Aviso|Registro truncado %1 de rastreamento gravados para a sessão de ETW com provedor %2. Dados de variáveis/anotações/usuários foram removidos|WFTracking|  
|[39459 - TrackingDataExtracted](39459-trackingdataextracted.md)|Detalhado|%1 Dados de acompanhamento extraídos na atividade %2.|WFRuntime|  
|[39460 - TrackingValueNotSerializable](39460-trackingvaluenotserializable.md)|Aviso|O argumento/variável extraídos “%1 " não é serializável.|WFTracking|  
|[57398 - MaxInstancesExceeded](57398-maxinstancesexceeded.md)|Aviso|O sistema atingiu o limite definido para o acelerador 'MaxConcurrentInstances'. O limite para este regulador de pressão foi definido como %1. O valor do acelerador pode ser alterado pela modificação do atributo 'maxConcurrentInstances' no elemento serviceThrottle ou modificando-se a propriedade 'MaxConcurrentInstances' no comportamento ServiceThrottlingBehavior.|WFServices|
