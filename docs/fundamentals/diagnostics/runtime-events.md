---
title: Eventos de tempo de execução
description: Examine os eventos de diagnóstico emitidos pelo tempo de execução do .NET (CoreCLR) que pode ser usado com ETW, LTTng ou EventPipe.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- runtime events (CoreCLR)
- ETW, EventPipe runtime events (CoreCLR)
ms.openlocfilehash: 33fa7275ce40934ce043b4d0dba5749c37515755
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "96585613"
---
# <a name="net-runtime-events"></a>Eventos de tempo de execução do .NET

O tempo de execução do .NET (CoreCLR) emite vários eventos que podem ser usados para diagnosticar problemas com seu aplicativo .NET que podem ser consumidos por meio de vários mecanismos, como, `ETW` `LTTng` e `EventPipe` .

Este documento serve como uma referência nos eventos que são acionados pelo tempo de execução do .NET Core.

Para eventos de tempo de execução no .NET Framework, consulte [eventos de ETW do CLR](../../framework/performance/clr-etw-events.md).

## <a name="in-this-section"></a>Nesta seção

[Eventos de contenção](runtime-contention-events.md)\
Esses eventos coletam informações sobre o monitoramento de contenções de bloqueio.

[Eventos de coleta de lixo](runtime-garbage-collection-events.md)\
 Esses eventos coletam informações referentes à coleta de lixo. Eles ajudam no diagnóstico e na depuração, incluindo a determinação de quantas vezes a coleta de lixo foi executada, a quantidade de memória liberada durante a coleta de lixo etc.

[Eventos de exceção](runtime-exception-events.md)\
Esses eventos de tempo de execução capturam informações sobre exceções que são geradas.

[Eventos de interoperabilidade](runtime-interop-events.md)\
Esses eventos de tempo de execução capturam informações sobre a geração de stubs Common Intermediate Language (CIL).

[Eventos do carregador e do fichário](runtime-loader-binder-events.md)\
Esses eventos coletam informações relacionadas ao carregamento e ao descarregamento de assemblies e módulos.

[Eventos de método](runtime-method-events.md)\
 Esses eventos coletam informações que são específicas para métodos. A carga desses eventos é necessária para resolução de símbolos. Além disso, esses eventos fornecem informações úteis, como o número de vezes que um método foi chamado.

[Eventos de thread](runtime-thread-events.md)\
 Esses eventos coletam informações sobre a função de trabalho e os threads de E/S.

[Eventos de tipo](runtime-type-events.md)\
Esses eventos coletam informações sobre o sistema de tipos.
