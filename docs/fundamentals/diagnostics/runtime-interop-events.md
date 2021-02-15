---
title: Eventos do Interop Runtime
description: Consulte eventos de tempo de execução do .NET que coletam informações de diagnóstico específicas à interoperabilidade.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- Interop events (CoreCLR)
- ETW, EventPipe, LTTng interop events (CoreCLR)
ms.openlocfilehash: 5635fb55b3a6ffa3f5611da80cdb2909e226e2ea
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "96585612"
---
# <a name="net-runtime-interop-events"></a>Eventos de interoperabilidade do .NET Runtime

Esses eventos de tempo de execução capturam informações sobre a geração de stubs Common Intermediate Language (CIL). Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

## <a name="ilstubgenerated-event"></a>Evento ILStubGenerated

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`InteropKeyword` (0x2000)|Informativo(4)|
  
|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ILStubGenerated`|88|Um stub de IL é gerado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt16`|O identificador de módulo.|
|`StubMethodID`|`win:UInt64`|O identificador do método de stub.|
|`StubFlags`|`win:UInt32`|Os sinalizadores para o stub:<br /><br /> `0x1` -Interoperabilidade reversa.<br /><br /> `0x2` -Interoperabilidade COM.<br /><br /> `0x4` -Stub gerado por NGen.exe.<br /><br /> `0x8` Delegá.<br /><br /> `0x10` -Argumento variável.<br /><br /> `0x20` -Receptor não gerenciado.<br /><br /> `0x40` -Estrutura de Marshal|
|`ManagedInteropMethodToken`|`win:UInt32`|O token para o método de interoperabilidade gerenciado.|
|`ManagedInteropMethodNameSpace`|`win:UnicodeString`|O namespace e o tipo de delimitador do método de interoperabilidade gerenciado.|
|`ManagedInteropMethodName`|`win:UnicodeString`|O nome do método de interoperabilidade gerenciado.|
|`ManagedInteropMethodSignature`|`win:UnicodeString`|A assinatura do método de interoperabilidade gerenciado.|
|`NativeMethodSignature`|`win:UnicodeString`|A assinatura do método nativo.|
|`StubMethodSignature`|`win:UnicodeString`|A assinatura do método de stub.|
|`StubMethodILCode`|`win:UnicodeString`|O código de Common Intermediate Language (CIL) para o método de stub.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|
