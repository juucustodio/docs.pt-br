---
title: Eventos de tempo de execução do ThreadPool
description: Consulte eventos de pool de threads de tempo de execução do .NET que coletam informações de diagnóstico sobre pool de threads no .NET Core Eventos de pool de threads são eventos de pool de threads de trabalho ou eventos de pool de threads de e/s
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- ThreadPool events (CoreCLR)
- ETW, thread pool events (CoreCLR)
ms.openlocfilehash: cdd6041c5842d4922c60e33daf6db366f7d35327
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96585637"
---
# <a name="net-runtime-thread-pool-events"></a>Eventos do pool de threads de tempo de execução .NET

Esses eventos coletam informações sobre threads de e/s de trabalho no ThreadPool. Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

## <a name="iothreadcreate_v1-event"></a>IOThreadCreate_V1 evento

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------------------------------|-----------|
|`IOThreadCreate_V1`|44|Um thread de E/S é criado no pool de threads.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Número de threads de E/S, incluindo o thread recém-criado.|
|`NumRetired`|`win:UInt64`|Número de threads de trabalho desativados.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="iothreadterminate_v1-event"></a>IOThreadTerminate_V1 evento

 A tabela a seguir mostra a palavra-chave e o nível

|Palavra-chave para acionar o evento|Level
|-----------------------------------|-----------
|`ThreadingKeyword` (0x10000)|Informativo (4)

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`IOThreadTerminate`|45|Um thread de e/s é encerrado no pool de threads.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Número de threads de E/S restantes no pool de threads.|
|`NumRetired`|`win:UInt64`|Número de threads de E/S desativados.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="iothreadretire_v1-event"></a>IOThreadRetire_V1 evento

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`IOThreadRetire_V1`|46|Um thread de E/S se torna um candidato para desativação.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Número de threads de E/S restantes no pool de threads.|
|`NumRetired`|`win:UInt64`|Número de threads de E/S desativados.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="iothreadunretire_v1-event"></a>IOThreadUnretire_V1 evento

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`IOThreadUnretire_V1`|47|Um thread de E/S é ativado novamente devido à E/S que chega em um período de espera depois que o thread se torna um candidato para desativação.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|Número de threads de E/S no pool de threads, incluindo esse.|
|`NumRetired`|`win:UInt64`|Número de threads de E/S desativados.|
|`ClrInstanceID`|`Win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadstart-event"></a>Evento ThreadPoolWorkerThreadStart

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadStart`|50|Um thread de trabalho é criado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho disponíveis para processar o trabalho, incluindo aqueles que já estão processando o trabalho.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho que não estão disponíveis para processar o trabalho, mas que estão sendo mantidos em reserva, caso mais threads sejam necessários posteriormente.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadstop-event"></a>Evento ThreadPoolWorkerThreadStop

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadStop`|51|Um thread de trabalho é interrompido.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho disponíveis para processar o trabalho, incluindo aqueles que já estão processando o trabalho.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho que não estão disponíveis para processar o trabalho, mas que estão sendo mantidos em reserva, caso mais threads sejam necessários posteriormente.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadwait-event"></a>Evento ThreadPoolWorkerThreadWait

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadWait`|57|Um thread de trabalho começa a aguardar o trabalho.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho disponíveis para processar o trabalho, incluindo aqueles que já estão processando o trabalho.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho que não estão disponíveis para processar o trabalho, mas que estão sendo mantidos em reserva, caso mais threads sejam necessários posteriormente.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadretirementstart-event"></a>Evento ThreadPoolWorkerThreadRetirementStart

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadRetirementStart`|52|Um thread de trabalho é desativado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho disponíveis para processar o trabalho, incluindo aqueles que já estão processando o trabalho.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho que não estão disponíveis para processar o trabalho, mas que estão sendo mantidos em reserva, caso mais threads sejam necessários posteriormente.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadretirementstop-event"></a>Evento ThreadPoolWorkerThreadRetirementStop

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadRetirementStop`|53|Um thread de trabalho desativado fica ativo novamente.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho disponíveis para processar o trabalho, incluindo aqueles que já estão processando o trabalho.|
|`RetiredWorkerThreadCount`|`win:UInt32`|Número de threads de trabalho que não estão disponíveis para processar o trabalho, mas que estão sendo mantidos em reserva, caso mais threads sejam necessários posteriormente.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadadjustmentsample-event"></a>Evento ThreadPoolWorkerThreadAdjustmentSample

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentSample`|54|Refere-se à coleta de informações para uma amostra; ou seja, uma medida da taxa de transferência com determinado nível de simultaneidade, em um instante.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Throughput`|`win:Double`|Número de conclusões por unidade de tempo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadadjustmentadjustment-event"></a>Evento ThreadPoolWorkerThreadAdjustmentAdjustment

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentAdjustment`|55|Registra uma alteração no controle, quando o algoritmo de injeção de threads (escalada) determina se uma alteração no nível de simultaneidade está em vigor.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AverageThroughput`|`win:Double`|Taxa de transferência média de uma amostra de medidas.|
|`NewWorkerThreadCount`|`win:UInt32`|Novo número de threads de trabalho ativos.|
|`Reason`|`win:UInt32`|Motivo do ajuste.<br /><br /> `0x0` Aquecimento.<br /><br /> `0x1` Inicializando.<br /><br /> `0x2` -Movimentação aleatória.<br /><br /> `0x3` -Movimentação de escalada.<br /><br /> `0x4` -Ponto de alteração.<br /><br /> `0x5` Estabiliza.<br /><br /> `0x6` Priva.<br /><br /> `0x7` -O thread atingiu o tempo limite.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolworkerthreadadjustmentstats-event"></a>Evento ThreadPoolWorkerThreadAdjustmentStats

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Detalhado (5)

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentStats`|56|Coleta de dados no pool de threads.|

 A tabela a seguir mostra os dados de evento

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Duration`|`win:Double`|Tempo, em segundos, durante o qual essas estatísticas foram coletadas.|
|`Throughput`|`win:Double`|Número médio de conclusões por segundo durante esse intervalo.|
|`ThreadWave`|`win:Double`|Reservado para uso interno.|
|`ThroughputWave`|`win:Double`|Reservado para uso interno.|
|`ThroughputErrorEstimate`|`win:Double`|Reservado para uso interno.|
|`AverageThroughputErrorEstimate`|`win:Double`|Reservado para uso interno.|
|`ThroughputRatio`|`win:Double`|A melhoria relativa na taxa de transferência causada por variações na contagem de threads de trabalho ativos durante esse intervalo.|
|`Confidence`|`win:Double`|Uma medida da validade do campo ThroughputRatio.|
|`NewcontrolSetting`|`win:Double`|O número de threads de trabalho ativos que servirão como a linha de base para variações futuras na contagem de threads ativos.|
|`NewThreadWaveMagnitude`|`win:UInt16`|A magnitude das variações futuras na contagem de threads ativos.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="threadpoolenqueue-event"></a>Evento ThreadPoolEnqueue

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Detalhado (5)

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolEnqueue`|61|Um item de trabalho foi enfileirado na fila do pool de threads.|

 A tabela a seguir mostra os dados de evento

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`WorkID`|`win:Pointer`|Ponteiro para a solicitação de trabalho.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="threadpooldequeue-event"></a>Evento ThreadPoolDequeue

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Detalhado (5)

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolDequeue`|62|Um item de trabalho foi removido da fila da fila do pool de threads.|

 A tabela a seguir mostra os dados de evento

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`WorkID`|`win:Pointer`|Ponteiro para a solicitação de trabalho.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="threadpoolioenqueue-event"></a>Evento ThreadPoolIOEnqueue

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Detalhado (5)

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolIOEnqueue`|63|Um thread enfileira uma notificação de conclusão de e/s depois que ocorre uma conclusão de e/s assíncrona.|

 A tabela a seguir mostra os dados de evento

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|Reservado para uso interno.|
|`Overlapped`|`win:Pointer`|Reservado para uso interno.|
|`MultiDequeues`|`win:Boolean`|Reservado para uso interno.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="threadpooliodequeue-event"></a>Evento ThreadPoolIODequeue

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Detalhado (5)

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolIODequeue`|64|Um thread desenfileira a notificação de conclusão de e/s.|

 A tabela a seguir mostra os dados de evento

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|Reservado para uso interno.|
|`Overlapped`|`win:Pointer`|Reservado para uso interno.|
|`MultiDequeues`|`win:Boolean`|Reservado para uso interno.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="threadpooliopack-event"></a>Evento ThreadPoolIOPack

 A tabela a seguir mostra a palavra-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Detalhado (5)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ThreadPoolIOPack`|65|O pacote de e/s sobreposto a ThreadPool é chamado.|

 A tabela a seguir mostra os dados de evento

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|Reservado para uso interno.|
|`Overlapped`|`win:Pointer`|Reservado para uso interno.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="threadcreating-event"></a>Evento ThreadCreating

 A tabela a seguir mostra as palavras-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`ThreadCreating`|70|O thread foi criado.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ID`|`win:Pointer`|ID do thread|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="threadrunning-event"></a>Evento ThreadRunning

 A tabela a seguir mostra as palavras-chave e o nível.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`ThreadRunning`|71|O thread começou a ser executado.|

 A tabela a seguir mostra os dados do evento.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ID`|`win:Pointer`|ID do thread|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|
