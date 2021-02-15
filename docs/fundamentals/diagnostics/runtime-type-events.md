---
title: Tipos de eventos de tempo de execução do sistema
description: Consulte eventos de tempo de execução do .NET que coletam informações de diagnóstico específicas para o sistema de tipo .NET, como TypeLoadStart e TypeLoadStop.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- type system events (CoreCLR)
- ETW, EventPipe, LTTng type system events (CoreCLR)
ms.openlocfilehash: 8eee89cddb0098da2cb449a4be21945adac725e3
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "96585609"
---
# <a name="net-runtime-type-events"></a>Eventos de tipo de tempo de execução .NET

Esses eventos coletam informações relacionadas aos tipos de carregamento. Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

## <a name="typeloadstart-event"></a>Evento TypeLoadStart

|Palavra-chave para acionar o evento|Evento|Level|  
|-----------------------------------|-----------|-----------|  
|`TypeDiagnosticKeyword` (0x8000000000)|Informativo (4)|  

|Evento|ID do evento|Descrição|  
|-----------|--------------|-----------------|  
|`TypeLoadStart`|73|Um carregamento de tipo foi iniciado.|

|Nome do campo|Tipo de dados|Descrição|  
|----------------|---------------|-----------------|  
|`TypeLoadStartID`|`win:UInt32`|ID para a operação de carregamento de tipo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|  

## <a name="typeloadstop-event"></a>Evento TypeLoadStop

|Palavra-chave para acionar o evento|Level|  
|-----------------------------------|-----------|-----------|  
|`TypeDiagnosticKeyword` (0x8000000000)|Informativo (4)|  

|Evento|ID do evento|Descrição|  
|-----------|--------------|-----------------|  
|`TypeLoadStop`|74|Uma carga de tipo foi concluída.|

|Nome do campo|Tipo de dados|Descrição|  
|----------------|---------------|-----------------|  
|`TypeLoadStartID`|`win:UInt32`|ID para a operação de carregamento de tipo (corresponde à TypeLoadStartID do evento TypeLoadStart correspondente).|
|`LoadLevel`|`win:UInt16`|Digite o nível de carga.|
|`TypeID`|`win:UInt64`|Ponteiro para a alça de tipo.|
|`TypeName`|`win:UnicodeString`|Nome do tipo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|  
