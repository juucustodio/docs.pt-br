---
description: 'Saiba mais sobre: Depurando enumerações'
title: Declarando enumerações
ms.date: 03/30/2017
helpviewer_keywords:
- debugging enumerations [.NET Framework]
- unmanaged enumerations [.NET Framework], debugging
- enumerations [.NET Framework debugging]
ms.assetid: 3af9f584-f1b4-4154-aeaa-8fce7c9f8b50
ms.openlocfilehash: 4a1d2fc9061fec7f5384418e4893c357f5d340ba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801417"
---
# <a name="debugging-enumerations"></a>Declarando enumerações

Esta seção descreve as enumerações não gerenciadas que a API de depuração utiliza.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Enumeração CLR_DEBUGGING_PROCESS_FLAGS](clr-debugging-process-flags-enumeration.md)  
 Fornece valores que são usados pelo método [ICLRDebugging:: OpenVirtualProcess](iclrdebugging-openvirtualprocess-method.md) .  
  
 [Enumeração CLRDataEnumMemoryFlags](clrdataenummemoryflags-enumeration.md)  
 Indica quais regiões de memória uma chamada para o método [ICLRDataEnumMemoryRegions:: EnumMemoryRegions](iclrdataenummemoryregions-enummemoryregions-method.md) deve incluir.  
  
 [Enumeração COR_PUB_ENUMPROCESS](cor-pub-enumprocess-enumeration.md)  
 Identifica o tipo de processo que será enumerado.  
  
 [Enumeração CorDebugBlockingReason](cordebugblockingreason-enumeration.md)  
 Especifica os motivos pelos quais um thread pode ficar bloqueado em um determinado objeto.  
  
 CorDebugChainReason  
 Indica o motivo ou os motivos para o início de uma cadeia de chamadas.  
  
 [Enumeração CorDebugCodeInvokeKind](cordebugcodeinvokekind-enumeration.md)  
 Descreve como uma função exportada invoca código gerenciado.  
  
 [Enumeração CorDebugCodeInvokePurpose](cordebugcodeinvokepurpose-enumeration.md)  
 Descreve por que uma função exportada chama código gerenciado.  
  
 CorDebugCreateProcessFlags  
 Fornece opções de depuração adicionais que podem ser usadas em uma chamada para o método [ICorDebug:: CreateProcess](icordebug-createprocess-method.md) .  
  
 [Enumeração CorDebugDebugEventKind](cordebugdebugeventkind-enumeration.md)  
 Indica o tipo de evento cujas informações são decodificadas pelo método [DecodeEvent](icordebugprocess6-decodeevent-method.md) .  
  
 [Enumeração CorDebugDecodeEventFlagsWindows](cordebugdecodeeventflagswindows-enumeration.md)  
 Fornece informações adicionais sobre eventos de depuração na plataforma Windows.  
  
 CorDebugExceptionCallbackType  
 Indica o tipo de retorno de chamada que é feito de um evento [ICorDebugManagedCallback2:: Exception](icordebugmanagedcallback2-exception-method.md) .  
  
 [Enumeração CorDebugExceptionFlags](cordebugexceptionflags-enumeration.md)  
 Fornece informações adicionais sobre uma exceção.  
  
 CorDebugExceptionUnwindCallbackType  
 Indica o evento que está sendo sinalizado pelo retorno de chamada durante a fase de desenrolamento.  
  
 [Enumeração CorDebugGCType](cordebuggctype-enumeration.md)  
 Indica se o coletor de lixo está sendo executado em uma estação de trabalho ou em um servidor.  
  
 [Enumeração CorDebugGenerationTypes](cordebuggenerationtypes-enumeration.md)  
 Especifica a geração de uma região de memória no heap gerenciado.  
  
 CorDebugHandleType  
 Indica o tipo de manipulação.  
  
 [Enumeração CorDebugIlToNativeMappingTypes](cordebugiltonativemappingtypes-enumeration.md)  
 Indica se uma faixa específica de instruções nativas corresponde a uma região de código especial.  
  
 CorDebugIntercept  
 Indica os tipos de código que podem ser entrados.  
  
 [Enumeração CorDebugInterfaceVersion](cordebuginterfaceversion-enumeration.md)  
 Especifica uma versão do .NET Framework ou a versão do .NET Framework na qual uma interface foi introduzida.  
  
 CorDebugInternalFrameType  
 Identifica o tipo de quadro de pilha.  
  
 [Enumeração CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md)  
 Contém valores que influenciam o comportamento do compilador just-in-time (JIT) gerenciado.  
  
 [Enumeração CorDebugJITCompilerFlagsDeprecated](cordebugjitcompilerflagsdeprecated-enumeration.md)  
 Obsoleto. `CORDEBUG_JIT_DEFAULT`Em vez disso, use o membro da enumeração [CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md) .  
  
 CorDebugMappingResult  
 Fornece os detalhes sobre como o valor do ponteiro de instrução (IP) foi obtido.  
  
 [Enumeração CorDebugMDAFlags](cordebugmdaflags-enumeration.md)  
 Especifica o status do thread no qual o assistente de depuração gerenciada (MDA) é disparado.  
  
 [Enumeração CorDebugNGenPolicy](cordebugngenpolicy-enumeration.md)  
 Fornece um valor que determina se um depurador carrega imagens nativas (NGen) do cache de imagens nativas.  
  
 [Enumeração CorDebugPlatform](cordebugplatform-enumeration.md)  
 Fornece valores de plataforma de destino que são usados pelo método [ICorDebugDataTarget:: GetPlatform](icordebugdatatarget-getplatform-method.md) .  
  
 [Enumeração CorDebugRecordFormat](cordebugrecordformat-enumeration.md)  
 Descreve o formato dos dados em uma matriz de bytes que contém informações sobre um evento de depuração de exceção nativo.  
  
 CorDebugRegister  
 Especifica os registros associados a uma determinada arquitetura de processador.  
  
 [Enumeração CorDebugSetContextFlag](cordebugsetcontextflag-enumeration.md)  
 Indica se o contexto é do quadro ativo (ou folha) na pilha ou se foi computado pelo desenrolamento de outro quadro.  
  
 [Enumeração CorDebugStateChange](cordebugstatechange-enumeration.md)  
 Descreve a quantidade de dados armazenados em cache que devem ser descartados com base em alterações no processo.  
  
 CorDebugStepReason  
 Indica o resultado de uma etapa individual.  
  
 CorDebugThreadState  
 Especifica o estado de um thread para depuração.  
  
 \>CorDebugUnmappedStop  
 Especifica o tipo de código não mapeado que pode disparar uma interrupção na execução do código pelo passador.  
  
 CorDebugUserState  
 Indica o estado do usuário de um thread.  
  
 [Enumeração CorGCReferenceType](corgcreferencetype-enumeration.md)  
 Identifica a fonte de um objeto para ser coletado do lixo.  
  
 [Enumeração ILCodeKind](ilcodekind-enumeration.md)  
 Fornece valores que especificam se o depurador é capaz de acessar variáveis locais ou o código incluído na instrumentação ReJIT do criador de perfis.  
  
 [Enumeração LoggingLevelEnum](logginglevelenum-enumeration.md)  
 Indica o nível de severidade de uma mensagem descritiva que é escrita no log de eventos quando um thread gerenciado registrar um evento.  
  
 [Enumeração LogSwitchCallReason](logswitchcallreason-enumeration.md)  
 Indica a operação que foi realizada em uma alternação entre depuração/rastreamento.  
  
 [Enumeração VariableLocationType](variablelocationtype-enumeration.md)  
 Indica o tipo de local nativo de uma variável.  
  
 [Enumeração WriteableMetadataUpdateMode](writeablemetadataupdatemode-enumeration.md)  
 Fornece valores que especificam se as atualizações na memória para metadados estão visíveis para um depurador.

 [Enumeração ClrDataSourceType](clrdatasourcetype-enumeration.md) Fornece valores que são usados pela estrutura de CLRDATA_IL_ADDRESS_MAP.

## <a name="related-sections"></a>Seções relacionadas  

 [Depurando coclasses](debugging-coclasses.md)  
  
 [Depurando interfaces](debugging-interfaces.md)  
  
 [Depurando funções estáticas globais](debugging-global-static-functions.md)  
  
 [Estruturas de depuração](debugging-structures.md)
