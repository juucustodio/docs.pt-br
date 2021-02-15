---
title: Eventos de tempo de execução de método
description: Consulte eventos de tempo de execução do .NET que coletam informações de diagnóstico específicas para métodos, como eventos de método CLR, marcador de método CLR ou eventos detalhados de método CLR e MethodJittingStarted.
ms.date: 11/13/2020
helpviewer_keywords:
- Method events (CoreCLR)
- ETW, EventPipe, LTTng method events (CoreCLR)
ms.openlocfilehash: f9d08efa420670cf7a8c863f115ff270998f2dca
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "96585610"
---
# <a name="net-runtime-method-events"></a>Eventos do método de tempo de execução do .NET

 Esses eventos coletam informações que são específicas para métodos. A carga desses eventos é necessária para resolução de símbolos. Além disso, esses eventos fornecem informações úteis, como métodos que são carregados e descarregados. Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

Todos os eventos de método têm um nível de "Informativo (4)". Todos os eventos detalhados do método têm um nível de "Detalhado (5)".

Todos os eventos de método são gerados pela palavra-chave `JITKeyword` (0x10) ou a palavra-chave `NGenKeyword` (0x20) no provedor de runtime ou então `JitRundownKeyword` (0x10) ou `NGENRundownKeyword` (0x20) com o provedor de encerramento.

As versões v2 desses eventos incluem o ReJITID, as versões v1 não.

## <a name="methodload_v1-event"></a>MethodLoad_V1 evento

A seguinte tabela mostra as informações do evento:

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodLoad_V1`|141|Gerado quando um método é carregado Just-In-Time (carregado via JIT) ou uma imagem NGEN é carregada. Métodos dinâmicos e genéricos não usam esta versão para carregamentos de método. Os auxiliares JIT nunca usam esta versão.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|Provedor de runtime `JITKeyword` (0x10)|Informativo (4)|
|Provedor de runtime `NGenKeyword` (0x20)|Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo de um método. Para métodos auxiliares JIT, isso é definido para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|Endereço inicial do método.|
|`MethodSize`|`win:UInt32`|Tamanho do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método de código com compilação JIT (de outro modo, código de imagem nativa NGEN).<br /><br /> 0x8: método auxiliar.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodload_v2-event"></a>MethodLoad_V2 evento

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`MethodLoad_V2`|141|Gerado quando um método é carregado Just-In-Time (carregado via JIT) ou uma imagem NGEN é carregada. Métodos dinâmicos e genéricos não usam esta versão para carregamentos de método. Os auxiliares JIT nunca usam esta versão.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|Provedor de runtime `JITKeyword` (0x10)|Informativo (4)|
|Provedor de runtime `NGenKeyword` (0x20)|Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo de um método. Para métodos auxiliares JIT, isso é definido para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|Endereço inicial do método.|
|`MethodSize`|`win:UInt32`|Tamanho do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método de código com compilação JIT (de outro modo, código de imagem nativa NGEN).<br /><br /> 0x8: método auxiliar.|
|`ReJITID`|`win:UInt64`|ID de ReJIT do método.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodunload_v1-event"></a>MethodUnLoad_V1 evento

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`MethodUnLoad_V1`|142|Gerado quando um módulo é descarregado ou um domínio do aplicativo é destruído. Métodos dinâmicos nunca usam essa versão para os descarregamentos de método.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10)|Informativo (4)|
|`NGenKeyword` 0x20|Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo de um método. Para métodos auxiliares JIT, isso é definido para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|Endereço inicial do método.|
|`MethodSize`|`win:UInt32`|Tamanho do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método de código com compilação JIT (de outro modo, código de imagem nativa NGEN).<br /><br /> 0x8: método auxiliar.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodunload_v2-event"></a>MethodUnLoad_V2 evento

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`MethodUnLoad_V2`|142|Gerado quando um módulo é descarregado ou um domínio do aplicativo é destruído. Métodos dinâmicos nunca usam essa versão para os descarregamentos de método.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10)|Informativo (4)|
|`NGenKeyword` 0x20|Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo de um método. Para métodos auxiliares JIT, isso é definido para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|Endereço inicial do método.|
|`MethodSize`|`win:UInt32`|Tamanho do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método de código com compilação JIT (de outro modo, código de imagem nativa NGEN).<br /><br /> 0x8: método auxiliar.|
|`ReJITID`|`win:UInt64`|ID de ReJIT do método.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="r2rgetentrypoint-event"></a>Evento R2RGetEntryPoint

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`R2RGetEntryPoint`|159|Gerado quando uma pesquisa de ponto de entrada do R2R termina.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Informativo (4)|
|`NGenKeyword` 0x20 |Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo de um método R2R.|
|`MethodNamespace`|`win:UnicodeString`|O namespace do método que está sendo pesquisado.|
|`MethodName`|`win:UnicodeString`|O nome do método que está sendo pesquisado.|
|`MethodSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipo).|
|`EntryPoint`|`win:UInt64`|O ponteiro para o ponto de entrada do método R2R|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="r2rgetentrypointstart-event"></a>Evento R2RGetEntryPointStart

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`R2RGetEntryPointStart`|160|Gerado quando uma pesquisa de ponto de entrada do R2R é iniciada.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Informativo (4)|
|`NGenKeyword` 0x20 |Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo de um método R2R.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodloadverbose_v1-event"></a>MethodLoadVerbose_V1 evento

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodLoadVerbose_V1`|143|Gerado quando um método é carregado via JIT ou uma imagem NGEN é carregada. Métodos dinâmicos e genéricos sempre usam esta versão para carregamentos de método. Os auxiliares JIT sempre usam esta versão.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Informativo (4)|
|`NGenKeyword` 0x20 |Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo do método. Para métodos auxiliares JIT, defina-o para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|O endereço inicial.|
|`MethodSize`|`win:UInt32`|O comprimento do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método com compilação JIT (de outro modo, gerado pelo NGen.exe)<br /><br /> 0x8: método auxiliar.|
|`MethodNameSpace`|`win:UnicodeString`|O nome completo do namespace associado ao método.|
|`MethodName`|`win:UnicodeString`|O nome de classe completo associado ao método.|
|`MethodSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipo).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodloadverbose_v2-event"></a>MethodLoadVerbose_V2 evento

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodLoadVerbose_V1`|143|Gerado quando um método é carregado via JIT ou uma imagem NGEN é carregada. Métodos dinâmicos e genéricos sempre usam esta versão para carregamentos de método. Os auxiliares JIT sempre usam esta versão.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Informativo (4)|
|`NGenKeyword` 0x20 |Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo do método. Para métodos auxiliares JIT, defina-o para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|O endereço inicial.|
|`MethodSize`|`win:UInt32`|O comprimento do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método com compilação JIT (de outro modo, gerado pelo NGen.exe)<br /><br /> 0x8: método auxiliar.|
|`MethodNameSpace`|`win:UnicodeString`|O nome completo do namespace associado ao método.|
|`MethodName`|`win:UnicodeString`|O nome de classe completo associado ao método.|
|`MethodSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipo).|
|`ReJITID`|`win:UInt64`|ID de ReJIT do método.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodunloadverbose_v1-event"></a>MethodUnLoadVerbose_V1 evento

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodUnLoadVerbose_V1`|144|Gerado quando um método dinâmico é destruído, um módulo é descarregado ou um domínio do aplicativo é destruído. Métodos dinâmicos sempre usam essa versão para os descarregamentos de método.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Informativo (4)|
|`NGenKeyword` 0x20 |Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo do método. Para métodos auxiliares JIT, defina-o para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|O endereço inicial.|
|`MethodSize`|`win:UInt32`|O comprimento do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método com compilação JIT (de outro modo, gerado pelo NGen.exe)<br /><br /> 0x8: método auxiliar.|
|`MethodNameSpace`|`win:UnicodeString`|O nome completo do namespace associado ao método.|
|`MethodName`|`win:UnicodeString`|O nome de classe completo associado ao método.|
|`MethodSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipo).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodunloadverbose_v2-event"></a>MethodUnLoadVerbose_V2 evento

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodUnLoadVerbose_V2`|144|Gerado quando um método dinâmico é destruído, um módulo é descarregado ou um domínio do aplicativo é destruído. Métodos dinâmicos sempre usam essa versão para os descarregamentos de método.|

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Informativo (4)|
|`NGenKeyword` 0x20 |Informativo (4)|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo do método. Para métodos auxiliares JIT, defina-o para o endereço inicial do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence (0 para auxiliares JIT).|
|`MethodStartAddress`|`win:UInt64`|O endereço inicial.|
|`MethodSize`|`win:UInt32`|O comprimento do método.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodFlags`|`win:UInt32`|0x1: método dinâmico.<br /><br /> 0x2: método genérico.<br /><br /> 0x4: método com compilação JIT (de outro modo, gerado pelo NGen.exe)<br /><br /> 0x8: método auxiliar.|
|`MethodNameSpace`|`win:UnicodeString`|O nome completo do namespace associado ao método.|
|`MethodName`|`win:UnicodeString`|O nome de classe completo associado ao método.|
|`MethodSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipo).|
|`ReJITID`|`win:UInt64`|ID de ReJIT do método.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodjittingstarted_v1-event"></a>MethodJittingStarted_V1 evento

A seguinte tabela mostra a palavra-chave e o nível:

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITKeyword` (0x10) |Detalhado (5)|
|`NGenKeyword` 0x20 |Detalhado (5)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodJittingStarted_V1`|145|Gerado quando um método está sendo compilado por JIT.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo do método.|
|`ModuleID`|`win:UInt64`|Identificador do módulo ao qual esse método pertence.|
|`MethodToken`|`win:UInt32`|0 para métodos dinâmicos e auxiliares JIT.|
|`MethodILSize`|`win:UInt32`|O tamanho do Common Intermediate Language (CIL) para o método que está sendo compilado em JIT.|
|`MethodNameSpace`|`win:UnicodeString`|O nome de classe completo associado ao método.|
|`MethodName`|`win:UnicodeString`|O nome do método.|
|`MethodSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipo).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodjitinliningsucceeded-event"></a>Evento MethodJitInliningSucceeded

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Detalhado (5)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodJitInliningSucceeded`|185|Gerado quando um método é embutido com êxito pelo compilador JIT.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Namespace do método que está sendo compilado.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nome do método que está sendo compilado.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipos) sendo compilados.|
|`InlinerNamespace`|`win:UnicodeString`|O namespace do método inlineer ("Parent").|
|`InlinerName`|`win:UnicodeString`|Nome do método embutido ("pai").|
|`InlinerNameSignature`|`win:UnicodeString`|Assinatura do método embutido ("pai") (lista separada por vírgulas de nomes de tipo).|
|`InlineeNamespace`|`win:UnicodeString`|O namespace do método embutir ("Child").|
|`InlineeName`|`win:UnicodeString`|Nome do método embutido ("Child").|
|`InlineeNameSignature`|`win:UnicodeString`|Assinatura do método embutido ("Child") (lista separada por vírgulas de nomes de tipo).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodjitinliningfailed-event"></a>Evento MethodJitInliningFailed

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Detalhado (5)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodJitInliningFailed`|192|Gerado quando um método não pôde ser embutido no compilador JIT.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Namespace do método que está sendo compilado.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nome do método que está sendo compilado.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipos) sendo compilados.|
|`InlinerNamespace`|`win:UnicodeString`|O namespace do método inlineer ("Parent").|
|`InlinerName`|`win:UnicodeString`|Nome do método embutido ("pai").|
|`InlinerNameSignature`|`win:UnicodeString`|Assinatura do método embutido ("pai") (lista separada por vírgulas de nomes de tipo).|
|`InlineeNamespace`|`win:UnicodeString`|O namespace do método embutir ("Child").|
|`InlineeName`|`win:UnicodeString`|Nome do método embutido ("Child").|
|`InlineeNameSignature`|`win:UnicodeString`|Assinatura do método embutido ("Child") (lista separada por vírgulas de nomes de tipo).|
|`FailAlways`|`win:Boolean`|Se o método está marcado como não inlinable.|
|`FailReason`|`win:UnicodeString`|Falha no alinhamento do motivo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodjittailcallsucceeded-event"></a>Evento MethodJitTailCallSucceeded

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Detalhado (5)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodJitTailCallSucceeded`|192|Gerado pelo compilador JIT quando um método pode ser chamado com êxito.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Namespace do método que está sendo compilado.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nome do método que está sendo compilado.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipos) sendo compilados.|
|`CallerNamespace`|`win:UnicodeString`|Namespace do método chamador.|
|`CallerName`|`win:UnicodeString`|Nome do método chamador.|
|`CallerNameSignature`|`win:UnicodeString`|Assinatura do método chamador (lista separada por vírgulas de nomes de tipo).|
|`CalleeNamespace`|`win:UnicodeString`|Namespace do método chamador.|
|`CalleeName`|`win:UnicodeString`|Nome do método chamador.|
|`CalleeNameSignature`|`win:UnicodeString`|Assinatura do método receptor (lista separada por vírgulas de nomes de tipo).|
|`TailPrefix`|`win:Boolean`|Se é uma instrução de prefixo final.|
|`TailCallType`|`win:UInt32`|O tipo de chamada tail.<br/><br/>0: chamada tail otimizada (epílogo + JMP)<br/><br/>1: chamada tail recursiva (o método tail chama a si mesmo)<br/><br/>2: chamada tail assistida pelo auxiliar|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodjittailcallfailed-event"></a>Evento MethodJitTailCallFailed

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JITTracingKeyword` 0x1000 |Detalhado (5)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`MethodJitTailCallFailed`|191|Gerado pelo compilador JIT quando um método falhou ao ser chamado como tail.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodBeingCompiledNamespace`|`win:UnicodeString`|Namespace do método que está sendo compilado.|
|`MethodBeingCompiledName`|`win:UnicodeString`|Nome do método que está sendo compilado.|
|`MethodBeingCompiledNameSignature`|`win:UnicodeString`|Assinatura do método (lista separada por vírgulas de nomes de tipos) sendo compilados.|
|`CallerNamespace`|`win:UnicodeString`|Namespace do método chamador.|
|`CallerNam`e|`win:UnicodeString`|Nome do método chamador.|
|`CallerNameSignature`|`win:UnicodeString`|Assinatura do método chamador (lista separada por vírgulas de nomes de tipo).|
|`CalleeNamespace`|`win:UnicodeString`|Namespace do método chamador.|
|`CalleeName`|`win:UnicodeString`|Nome do método chamador.|
|`CalleeNameSignature`|`win:UnicodeString`|Assinatura do método receptor (lista separada por vírgulas de nomes de tipo).|
|`TailPrefix`|`win:Boolean`|Se é uma instrução de prefixo final.|
|`FailReason`|`win:UnicodeString`|Falha na chamada de cauda do motivo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="methodiltonativemap-event"></a>Evento MethodILToNativeMap

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|
|`JittedMethodILToNativeMapKeyword` (0x20000) |Detalhado (5)|

|Evento|ID do evento|Descrição|
|----------------|---------------|-----------------|
|`MethodILToNativeMap`|190|Mapeia o evento de mapa IL-to-Native para métodos compilados por JIT.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`MethodID`|`win:UInt64`|Identificador exclusivo de um método.|
|`ReJITID`|`win:UInt64`|A ID de ReJIT do método.|
|`MethodExtent`|`win:UInt8`|A extensão do método com compilação JIT.|
|`CountOfMapEntries`|`win:UInt8`|Número de entradas de mapa|
|`ILOffsets`|`win:UInt32`|O deslocamento de IL.|
|`NativeOffsets`|`win:UInt32`|O deslocamento de código nativo.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|
