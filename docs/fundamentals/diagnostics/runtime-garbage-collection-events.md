---
title: Eventos de tempo de execução de coleta de lixo
description: Consulte eventos de tempo de execução do .NET que coletam informações de diagnóstico específicas para o coletor de lixo do .NET.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- GC events
- garbage collection events (CoreCLR)
- ETW, EventPipe, LTTng garbage collection events (CoreCLR)
ms.openlocfilehash: 2799a93f351baf23ec7a359b0b4b2be5c216dc4d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "96585615"
---
# <a name="net-runtime-garbage-collection-events"></a>Eventos de coleta de lixo do .NET Runtime

 Esses eventos coletam informações referentes à coleta de lixo. Eles ajudam no diagnóstico e na depuração, incluindo a determinação de quantas vezes a coleta de lixo foi executada, a quantidade de memória liberada durante a coleta de lixo etc. Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

## <a name="gcstart_v2-event"></a>GCStart_V2 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCStart_V1`|1|Uma coleta de lixo foi iniciada.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|A *n*° de coleta de lixo.|
|`Depth`|`win:UInt32`|A geração que está sendo coletada.|
|`Reason`|`win:UInt32`|Motivo do gatilho da coleta de lixo:<br /><br /> `0x0` -Alocação de heap de objeto pequeno.<br /><br /> `0x1` Induzida.<br /><br /> `0x2` -Memória insuficiente.<br /><br /> `0x3` Esvaziá.<br /><br /> `0x4` -Alocação de heap de objeto grande.<br /><br /> `0x5` -Sem espaço (para heap de objeto pequeno).<br /><br /> `0x6` -Sem espaço (para heap de objeto grande).<br /><br /> `0x7` -Induzido, mas não forçado como bloqueio.|
|`Type`|`win:UInt32`|`0x0` -A coleta de lixo de bloqueio ocorreu fora da coleta de lixo em segundo plano.<br /><br /> `0x1` -Coleta de lixo em segundo plano.<br /><br /> `0x2` -A coleta de lixo de bloqueio ocorreu durante a coleta de lixo em segundo plano.|
|`ClrInstanceID`|win:UInt16|ID exclusiva para a instância do CoreCLR.|

## <a name="gcend_v1-event"></a>Evento GCEnd_V1

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCEnd_V1`|2|A coleta de lixo foi encerrada.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|A *n*° de coleta de lixo.|
|`Depth`|`win:UInt32`|A geração que foi coletada.|
|`ClrInstanceID`|win:UInt16|ID exclusiva para a instância do CoreCLR.|

## <a name="gcheapstats_v2-event"></a>GCHeapStats_V2 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`GCHeapStats_V2`|4|Mostra as estatísticas de heap no final de cada coleta de lixo.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`GenerationSize0`|`win:UInt64`|O tamanho, em bytes, da memória de geração 0.|
|`TotalPromotedSize0`|`win:UInt64`|O número de bytes que são promovidos da geração 0 para a geração 1.|
|`GenerationSize1`|`win:UInt64`|O tamanho, em bytes, da memória de geração 1.|
|`TotalPromotedSize1`|`win:UInt64`|O número de bytes que são promovidos da geração 1 para a geração 2.|
|`GenerationSize2`|`win:UInt64`|O tamanho, em bytes, da memória de geração 2.|
|`TotalPromotedSize2`|`win:UInt64`|O número de bytes que sobreviveram na geração 2 após a última coleta.|
|`GenerationSize3`|`win:UInt64`|O tamanho, em bytes, do heap de objetos grandes.|
|`TotalPromotedSize3`|`win:UInt64`|O número de bytes que sobreviveram no heap de objetos grandes após a última coleta.|
|`FinalizationPromotedSize`|`win:UInt64`|O tamanho total, em bytes, dos objetos que estão prontos para finalização.|
|`FinalizationPromotedCount`|`win:UInt64`|O número de objetos que estão prontos para finalização.|
|`PinnedObjectCount`|`win:UInt32`|O número de objetos (imóveis) fixados.|
|`SinkBlockCount`|`win:UInt32`|O número de blocos de sincronização em uso.|
|`GCHandleCount`|`win:UInt32`|O número de manipuladores de coleta de lixo em uso.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|
|`GenerationSize4`|`win:UInt64`|O tamanho, em bytes, do heap de objeto fixado.|
|`TotalPromotedSize4`|`win:UInt64`|O número de bytes que sobreviveram no heap de objeto fixado após a última coleta.|

## <a name="gccreatesegment_v1-event"></a>GCCreateSegment_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCCreateSegment_V1`|5|Um novo segmento de coleta de lixo foi criado. Além disso, quando o rastreamento é habilitado em um processo que já está em execução, esse evento é acionado para cada segmento existente.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|O endereço do segmento.|
|`Size`|`win:UInt64`|O tamanho do segmento.|
|`Type`|`win:UInt32`|0x0 – Heap de objetos pequenos.<br /><br /> 0x1 – Heap de objetos grandes.<br /><br /> 0x2 – Heap somente leitura.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

Observe que o tamanho de segmentos alocados pelo coletor de lixo é específico à implementação e está sujeito a alterações a qualquer momento, incluindo em atualizações periódicas. Seu aplicativo nunca deve fazer suposições sobre o tamanho de um segmento em particular nem depender dele, tampouco deve tentar configurar a quantidade de memória disponível para alocações de segmento.

## <a name="gcfreesegment_v1-event"></a>GCFreeSegment_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCFreeSegment_V1`|6|Um segmento de coleta de lixo foi liberado.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|O endereço do segmento.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="gcrestarteebegin_v1-event"></a>GCRestartEEBegin_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCRestartEEBegin_V1`|7|A continuidade da suspensão do Common Language Runtime foi iniciada.|

Esse evento não tem nenhum dado de evento.

## <a name="gcrestarteeend_v1-event"></a>GCRestartEEEnd_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCRestartEEEnd_V1`|3|A continuidade da suspensão do Common Language Runtime foi encerrada.|

Esse evento não tem nenhum dado de evento.

## <a name="gcsuspendeeend_v1-event"></a>GCSuspendEEEnd_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCSuspendEEEnd_V1`|8|Fim da suspensão do mecanismo de execução da coleta de lixo.|

Esse evento não tem nenhum dado de evento.

## <a name="gcsuspendeebegin_v1-event"></a>GCSuspendEEBegin_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCSuspendEEBegin_V1`|8|Início da suspensão do mecanismo de execução da coleta de lixo.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|A *n*° de coleta de lixo.|
|`Reason`|`win:UInt32`|Motivo da suspensão de EE.<br/><br/>`0x0`: Suspender para outros<br/><br/>`0x1`: Suspender para GC.<br/><br/>`0x2`: Suspender para desligamento de AppDomain.<br/><br/>`0x3`: Suspender para a densidade de código.<br/><br/>`0x4`: Suspender para desligamento.<br/><br/>`0x5`: Suspender para o depurador.<br/><br/>`0x6`: Suspender para o CG Prep.<br/><br/>`0x7`: Suspender para varredura do depurador|

## <a name="gcallocationtick_v3-event"></a>GCAllocationTick_V3 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Detalhado (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCAllocationTick_V3`|10|A cada vez, aproximadamente 100 KB são alocados.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AllocationAmount`|`win:UInt32`|O tamanho de alocação, em bytes. Esse valor é preciso para alocações menores do que o tamanho de um ULONG (4.294.967.295 bytes). Se a alocação for maior, esse campo conterá um valor truncado. Use `AllocationAmount64` para alocações muito grandes.|
|`AllocationKind`|`win:UInt32`|`0x0` -Alocação de objeto pequeno (a alocação está em heap de objeto pequeno).<br /><br /> `0x1` -Alocação de objeto grande (a alocação está em heap de objeto grande).|
|`AllocationAmount64`|`win:UInt64`|O tamanho de alocação, em bytes. Esse valor é preciso para alocações muito grandes.|
|`TypeId`|`win:Pointer`|O endereço da MethodTable. Quando há vários tipos de objetos que foram alocados durante esse evento, esse é o endereço da MethodTable que corresponde ao último objeto alocado (o objeto que fez com que o limite de 100 KB fosse excedido).|
|`TypeName`|`win:UnicodeString`|O nome do tipo que foi alocado. Quando há vários tipos de objetos que foram alocados durante esse evento, esse é o tipo do último objeto alocado (o objeto que fez com que o limite de 100 KB fosse excedido).|
|`HeapIndex`|`win:UInt32`|O heap em que o objeto foi alocado. Esse valor é 0 (zero) durante a execução da coleta de lixo da estação de trabalho.|
|`Address`|`win:Pointer`|O endereço do último objeto alocado.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="gccreateconcurrentthread_v1-event"></a>GCCreateConcurrentThread_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCCreateConcurrentThread_V1`|11|O thread da coleta de lixo simultânea foi criado.|

Esse evento não tem nenhum dado de evento.

## <a name="gcterminateconcurrentthread_v1-event"></a>GCTerminateConcurrentThread_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|
|`ThreadingKeyword` (0x10000)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCTerminateConcurrentThread_V1`|12|O thread da coleta de lixo simultânea foi terminado.|

Esse evento não tem nenhum dado de evento.

## <a name="gcfinalizersbegin_v1-event"></a>GCFinalizersBegin_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCFinalizersBegin_V1`|14|O início da execução dos finalizadores.|

Esse evento não tem nenhum dado de evento.

## <a name="gcfinalizersend_v1-event"></a>GCFinalizersEnd_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCFinalizersEnd_V1`|13|O fim da execução dos finalizadores.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|O número de finalizadores que foram executados.|
|`ClrInstanceID`|win:UInt16|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="setgchandle-event"></a>Evento setgchandle

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCHandleKeyword` 0x2|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`SetGCHandle`|30|Um identificador de GC foi definido.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|O endereço do identificador alocado.|
|`ObjectID`|`win:Pointer`|O endereço do objeto cujo identificador foi criado.|
|`Kind`|`win:UInt32`|O tipo de identificador de GC que foi definido. <br /><br />`0x0`: WeakShort <br/><br/>`0x1`: WeakLong <br /><br />`0x2`: Forte <br /><br />`0x3`: Fixado <br /><br />`0x4`: Variável<br /><br />`0x5`: RefCounted <br /><br />`0x6`: Dependente<br /><br />`0x7`: AsyncPinned<br /><br />`0x8`: Identificador sizedref|
|`Generation`|`win:UInt32`|A geração do objeto cujo identificador foi criado.|
|`AppDomainID`|`win:UInt64`|A ID do AppDomain.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="destroygchandle-event"></a>Evento DestroyGCHandle

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCHandleKeyword` 0x2|Informativo (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`DestroyGCHandle`|31|Um identificador de GC é destruído.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|O endereço do identificador destruído.|
|`ClrInstanceID`|win:UInt16|ID exclusiva para a instância do CoreCLR.|

## <a name="pinobjectatgctime-event"></a>Evento PinObjectAtGCTime

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Detalhado (5)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`PinObjectAtGCTime`|33|Um objeto foi fixado durante um GC.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|O endereço do identificador.|
|`ObjectID`|`win:Pointer`|O endereço do objeto fixado.|
|`ObjectSize`|`win:UInt64`|O tamanho do objeto fixado.|
|`TypeName`|`win:UnicodeString`|O nome do tipo do objeto fixado.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="gctriggered-event"></a>Evento GCTriggered

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Detalhado (5)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCTriggered`|33|Um GC foi disparado.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Reason`|`win:UInt32`|O motivo pelo qual um GC foi disparado.<br/><br/>`0x0`: AllocSmall<br/><br/>`0x1`: Induzido <br/><br/>`0x2`: LowMemory <br/><br/>`0x3`: Vazio <br/><br/>`0x4`: AllocLarge <br/><br/>`0x5`: OutOfSpaceSmallObjectHeap <br/><br/>`0x6`: OutOfSpaceLargeObjectHeap <br/><br/>`0x7`:InducedNoForce <br/><br/>`0x8`: Estresse <br/><br/>`0x9`: InducedLowMemory|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="increasememorypressure-event"></a>Evento IncreaseMemoryPressure

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informações (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|----------------|---------------|-----------------|
|`IncreaseMemoryPressure`|200|A pressão de memória foi aumentada.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ClrInstanceID`|win:UInt16|ID exclusiva para a instância do CoreCLR.|

## <a name="decreasememorypressure-event"></a>Evento DecreaseMemoryPressure

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informações (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|----------------|---------------|-----------------|
|`DecreaseMemoryPressure`|201|A pressão de memória foi reduzida.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`BytesFreed`|`win:UInt32`|Bytes liberados.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="gcmarkwithtype-event"></a>Evento GCMarkWithType

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Informações (4)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|----------------|---------------|-----------------|
|`GCMarkWithType`|202|Uma raiz GC foi marcada durante A fase de marca do GC.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`HeapNum`|`win:UInt32`|O número do heap.|
|`ClrInstanceID`|win:UInt16|ID exclusiva para a instância do CoreCLR.|
|`Type`|`win:UInt32`|O tipo de raiz do GC.<br/><br/>`0x0`: Pilha<br/><br/>`0x1`: Finalizador<br/><br/>`0x2`: Identificador<br/><br/>`0x3`: Mais antigo<br/><br/>`0x4`: Identificador sizedref<br/><br/>`0x5`: Estouro<br/><br/>|
|`Bytes`|`win:UInt64`|O número de bytes marcados.|

## <a name="gcjoin_v2-event"></a>GCJoin_V2 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|Detalhado (5)|

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`GCJoin_V2`|203|Um thread GC ingressado.|

A seguinte tabela mostra os dados do evento:

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Heap`|`win:UInt32`|O número do heap|
|`JoinTime`|`win:UInt32`|Indica se este evento é acionado no início de uma junção ou término de uma junção ( `0x0` para o início da junção, `0x1` para término da junção)|
|`JoinType`|`win:UInt32`|O tipo de junção. <br/><br/>`0x0`: Última junção<br/><br/>`0x1`: Junção <br/><br/>`0x2`: Reiniciar <br/><br/>`0x3`: Primeira junção inversa<br/><br/>`0x4`: Junção inversa<br/><br/>|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|
