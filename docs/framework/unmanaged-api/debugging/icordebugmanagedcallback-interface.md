---
description: 'Saiba mais sobre: interface ICorDebugManagedCallback'
title: Interface ICorDebugManagedCallback
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback
helpviewer_keywords:
- ICorDebugManagedCallback interface [.NET Framework debugging]
ms.assetid: b47f1d61-c7dc-4196-b926-0b08c94f7041
topic_type:
- apiref
ms.openlocfilehash: 0dd33e4295caa8f5ae41c65d9bd10152737156ca
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99722809"
---
# <a name="icordebugmanagedcallback-interface"></a>Interface ICorDebugManagedCallback

Fornece métodos para processar retornos de chamada do depurador.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Break](icordebugmanagedcallback-break-method.md)|Notifica o depurador quando uma <xref:System.Reflection.Emit.OpCodes.Break> instrução no fluxo de código é executada.|  
|[Método Breakpoint](icordebugmanagedcallback-breakpoint-method.md)|Notifica o depurador quando um ponto de interrupção é encontrado.|  
|[Método BreakpointSetError](icordebugmanagedcallback-breakpointseterror-method.md)|Notifica o depurador de que o Common Language Runtime (CLR) não pôde associar com precisão um ponto de interrupção que foi definido antes de uma função ser compilada por JIT (just-in-time).|  
|[Método ControlCTrap](icordebugmanagedcallback-controlctrap-method.md)|Notifica o depurador de que um CTRL + C é interceptado no processo que está sendo depurado.|  
|[Método CreateAppDomain](icordebugmanagedcallback-createappdomain-method.md)|Notifica o depurador de que um domínio de aplicativo foi criado.|  
|[Método CreateProcess](icordebugmanagedcallback-createprocess-method.md)|Notifica o depurador quando um processo foi anexado ou iniciado pela primeira vez.|  
|[Método CreateThread](icordebugmanagedcallback-createthread-method.md)|Notifica o depurador de que um thread iniciou a execução de código gerenciado.|  
|[Método DebuggerError](icordebugmanagedcallback-debuggererror-method.md)|Notifica o depurador de que ocorreu um erro ao tentar lidar com um evento do CLR.|  
|[Método EditAndContinueRemap](icordebugmanagedcallback-editandcontinueremap-method.md)|Preterido. Notifica o depurador de que um evento de remapeamento foi enviado para o IDE.|  
|[Método EvalComplete](icordebugmanagedcallback-evalcomplete-method.md)|Notifica o depurador de que uma avaliação foi concluída.|  
|[Método EvalException](icordebugmanagedcallback-evalexception-method.md)|Notifica o depurador de que uma avaliação foi encerrada com uma exceção sem tratamento.|  
|[Método Exception](icordebugmanagedcallback-exception-method.md)|Notifica o depurador de que uma exceção foi lançada do código gerenciado.|  
|[Método ExitAppDomain](icordebugmanagedcallback-exitappdomain-method.md)|Notifica o depurador de que um domínio de aplicativo foi encerrado.|  
|[Método ExitProcess](icordebugmanagedcallback-exitprocess-method.md)|Notifica o depurador de que um processo foi encerrado.|  
|[Método ExitThread](icordebugmanagedcallback-exitthread-method.md)|Notifica o depurador de que um thread que estava executando código gerenciado foi encerrado.|  
|[Método LoadAssembly](icordebugmanagedcallback-loadassembly-method.md)|Notifica o depurador de que um assembly CLR foi carregado com êxito.|  
|[Método LoadClass](icordebugmanagedcallback-loadclass-method.md)|Notifica o depurador de que uma classe foi carregada.|  
|[Método LoadModule](icordebugmanagedcallback-loadmodule-method.md)|Notifica o depurador de que um módulo CLR foi carregado com êxito.|  
|[Método LogMessage](icordebugmanagedcallback-logmessage-method.md)|Notifica o depurador de que um thread gerenciado pelo CLR chamou um método na <xref:System.Diagnostics.EventLog> classe para registrar um evento.|  
|[Método LogSwitch](icordebugmanagedcallback-logswitch-method.md)|Notifica o depurador de que um thread gerenciado pelo CLR chamou um método na <xref:System.Diagnostics.Switch> classe para criar, modificar ou excluir uma opção de depuração/rastreamento.|  
|[Método NameChange](icordebugmanagedcallback-namechange-method.md)|Notifica o depurador de que o nome de um domínio de aplicativo ou thread foi alterado.|  
|[Método StepComplete](icordebugmanagedcallback-stepcomplete-method.md)|Notifica o depurador de que uma etapa foi concluída.|  
|[Método UnloadAssembly](icordebugmanagedcallback-unloadassembly-method.md)|Notifica o depurador de que um assembly CLR foi descarregado.|  
|[Método UnloadClass](icordebugmanagedcallback-unloadclass-method.md)|Notifica o depurador de que uma classe está sendo descarregada.|  
|[Método UnloadModule](icordebugmanagedcallback-unloadmodule-method.md)|Notifica o depurador de que um módulo CLR (DLL) foi descarregado.|  
|[Método UpdateModuleSymbols](icordebugmanagedcallback-updatemodulesymbols-method.md)|Notifica o depurador de que os símbolos de um módulo CLR foram alterados.|  
  
## <a name="remarks"></a>Comentários  

 Todos os retornos de chamada são serializados, chamados no mesmo thread e chamados com o processo no estado SYNCHRONIZED.  
  
 Cada implementação de retorno de chamada deve chamar [ICorDebugController:: Continue](icordebugcontroller-continue-method.md) para retomar a execução. Se `ICorDebugController::Continue` não for chamado antes que o retorno de chamada seja retornado, o processo permanecerá parado e nenhum mais retornos de chamada de evento ocorrerá até que `ICorDebugController::Continue` seja chamado.  
  
 Um depurador deve implementar [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md) se estiver depurando .NET Framework aplicativos da versão 2,0. Uma instância do `ICorDebugManagedCallback` ou `ICorDebugManagedCallback2` é passada como o objeto de retorno de chamada para [ICorDebug:: SetManagedHandler](icordebug-setmanagedhandler-method.md).  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebug](icordebug-interface.md)
- [Interface ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
