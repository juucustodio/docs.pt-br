---
title: Eventos de tempo de execução de exceção
description: Consulte eventos de tempo de execução do .NET que coletam informações de diagnóstico específicas para exceções e tratamento de exceções.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- exception events (CoreCLR)
- exception handling events (CoreCLR)
- ETW, EventPipe, LTTng exception events (CoreCLR)
ms.openlocfilehash: f4f63c8469f9c734b872ddaec8d1d7f7f0427576
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96585631"
---
# <a name="net-runtime-exception-events"></a>Eventos de exceção de tempo de execução .NET

Esses eventos de tempo de execução capturam informações sobre exceções que são geradas. Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

## <a name="exceptionthrown_v1-event"></a>ExceptionThrown_V1 evento

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Erro (1)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionThrown_V1`|80|Uma exceção gerenciada é gerada.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ExceptionType`|`win:UnicodeString`|Tipo da exceção; por exemplo, `System.NullReferenceException`.|
|`ExceptionMessage`|`win:UnicodeString`|A mensagem de exceção real.|
|`EIPCodeThrow`|`win:Pointer`|Ponteiro de instrução em que ocorreu a exceção.|
|`ExceptionHR`|`win:UInt32`|Exceção [HRESULT](/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a).|
|`ExceptionFlags`|`win:UInt16`|`0x01`: HasInnerException.<br /><br /> `0x02`: Isaninhaexception.<br /><br /> `0x04`: IsRethrownException.<br /><br /> `0x08`: IsCorruptedStateException (indica que o estado do processo está corrompido; consulte [tratamento de exceções de estado corrompido](/archive/msdn-magazine/2009/february/clr-inside-out-handling-corrupted-state-exceptions)).<br /><br /> `0x10`: IsCLSCompliant (uma exceção derivada de <xref:System.Exception> é compatível com CLS; caso contrário, não é compatível com CLS).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="exceptioncatchstart-event"></a>Evento ExceptionCatchStart

Esse evento é emitido quando um manipulador de catch de exceção gerenciada começa.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionCatchStart`|250|Uma exceção gerenciada é tratada pelo tempo de execução.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|Ponteiro de instrução em que ocorreu a exceção.|
|`MethodID`|`win:Pointer`|Ponteiro para o descritor de método no método em que ocorreu a exceção.|
|`MethodName`|`win:UnicodeString`|Nome do método em que ocorreu a exceção.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="exceptioncatchstop-event"></a>Evento ExceptionCatchStop

Esse evento é emitido quando um manipulador de captura de exceção gerenciada termina.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionCatchStop`|251|Um manipulador de captura de exceção gerenciada é feito.|

## <a name="exceptionfinallystart-event"></a>Evento ExceptionFinallyStart

Esse evento é emitido quando um manipulador de exceção gerenciada finally é iniciado.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionFinallyStart`|252|Uma exceção gerenciada é tratada pelo tempo de execução.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|Ponteiro de instrução em que ocorreu a exceção.|
|`MethodID`|`win:Pointer`|Ponteiro para o descritor de método no método em que ocorreu a exceção.|
|`MethodName`|`win:UnicodeString`|Nome do método em que ocorreu a exceção.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|

## <a name="exceptionfinallystop-event"></a>Evento ExceptionFinallyStop

Esse evento é emitido quando um manipulador de captura de exceção gerenciada termina.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionFinallyStop`|253|Um manipulador de exceção gerenciada finally é feito.|

## <a name="exceptionfilterstart-event"></a>Evento ExceptionFilterStart

Esse evento é emitido quando uma filtragem de exceção gerenciada é iniciada.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionFilterStart`|254|Uma filtragem de exceção gerenciada começa.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|Ponteiro de instrução em que ocorreu a exceção.|
|`MethodID`|`win:Pointer`|Ponteiro para o descritor de método no método em que ocorreu a exceção.|
|`MethodName`|`win:UnicodeString`|Nome do método em que ocorreu a exceção.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="exceptionfilterstop-event"></a>Evento ExceptionFilterStop

Esse evento é emitido quando uma filtragem de exceção gerenciada termina.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Informativo (4)|

 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionFilteringStart`|255|Uma filtragem de exceção gerenciada termina.|

## <a name="exceptionthrownstop-event"></a>Evento ExceptionThrownStop

Esse evento é emitido quando o tempo de execução é realizado tratando uma exceção gerenciada que foi lançada.

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`ExceptionKeyword` (0x8000)|Informativo (4)|
  
 A tabela a seguir mostra as informações do evento.

|Evento|ID do evento|Acionado quando|
|-----------|--------------|-----------------|
|`ExceptionThrownStop`|256|Uma filtragem de exceção gerenciada termina.|
