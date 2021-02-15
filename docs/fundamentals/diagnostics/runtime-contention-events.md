---
title: Monitorar eventos de tempo de execução de contenção de bloqueio
description: Consulte eventos de ETW que coletam informações específicas para as contenções de bloqueio do monitor.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- monitor lock contention events (CoreCLR)
- ETW, EventPipe, LTTng contention events (CoreCLR)
ms.openlocfilehash: 38e5f493d4b223b4839dbd6f814cf656722189b2
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "96585614"
---
# <a name="net-runtime-contention-events"></a>Eventos de contenção do tempo de execução do .NET

Esses eventos de tempo de execução capturam informações sobre contenções de bloqueio de monitor, como with `Monitor.Enter` ou a palavra-chave C# lock. Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

## <a name="contentionstart_v1-event"></a>ContentionStart_V1 evento

Esse evento é emitido no início de uma contenção de bloqueio de monitor.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ContentionKeyword` (0x4000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ContentionStart_V1`|81|Uma contenção de bloqueio de monitor é iniciada.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Flags`|`win:UInt8`|`0` para gerenciado; `1` para nativo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="contentionstop_v1-event"></a>ContentionStop_V1 evento

Esse evento é emitido no final de uma contenção de bloqueio de monitor.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ContentionKeyword` (0x4000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ContentionStop_V1`|91|Uma contenção de bloqueio de monitor termina.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`Flags`|`win:UInt8`|`0` para gerenciado; `1` para nativo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|
|`DurationNs`|`win:Double`|Duração da contenção em nanossegundos.|
