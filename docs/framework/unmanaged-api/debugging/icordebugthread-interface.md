---
description: 'Saiba mais sobre: interface ICorDebugThread'
title: Interface ICorDebugThread
ms.date: 03/30/2017
api_name:
- ICorDebugThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread
helpviewer_keywords:
- ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 3930fd9b-2bc3-4b72-80a0-b6eeb94d60c6
topic_type:
- apiref
ms.openlocfilehash: 7e16fa2a82a004a5c85d60a278cdd14df6ab2300
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658822"
---
# <a name="icordebugthread-interface"></a>Interface ICorDebugThread

Representa um thread em um processo. O tempo de vida de uma instância `ICorDebugThread` é igual ao tempo de vida do thread que ela representa.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método ClearCurrentException](icordebugthread-clearcurrentexception-method.md)|Este método não está implementado. Não o use.|  
|[Método CreateEval](icordebugthread-createeval-method.md)|Cria um objeto ICorDebugEval que opera sobre isso `ICorDebugThread` .|  
|[Método CreateStepper](icordebugthread-createstepper-method.md)|Cria um objeto ICorDebugStepper que permite percorrer o quadro ativo neste `ICorDebugThread` .|  
|[Método EnumerateChains](icordebugthread-enumeratechains-method.md)|Obtém um ponteiro de interface para um enumerador ICorDebugChainEnum que contém todas as cadeias de pilha neste `ICorDebugThread` .|  
|[Método GetActiveChain](icordebugthread-getactivechain-method.md)|Obtém um ponteiro de interface para o ICorDebugChain ativo neste `ICorDebugThread` .|  
|[Método GetActiveFrame](icordebugthread-getactiveframe-method.md)|Obtém um ponteiro de interface para o ICorDebugFrame ativo neste `ICorDebugThread` .|  
|[Método GetAppDomain](icordebugthread-getappdomain-method.md)|Obtém um ponteiro de interface para o domínio do aplicativo no qual `ICorDebugThread` está sendo executado no momento.|  
|[Método GetCurrentException](icordebugthread-getcurrentexception-method.md)|Obtém um ponteiro de interface para um objeto ICorDebugValue que representa uma exceção que está sendo lançada atualmente pelo código gerenciado.|  
|[Método GetDebugState](icordebugthread-getdebugstate-method.md)|Obtém um valor de CorDebugThreadState que descreve o estado de depuração atual disso `ICorDebugThread` .|  
|[Método GetHandle](icordebugthread-gethandle-method.md)|Obtém o identificador atual da parte ativa deste `ICorDebugThread` .|  
|[Método GetID](icordebugthread-getid-method.md)|Obtém o identificador do sistema operacional atual da parte ativa deste `ICorDebugThread` .|  
|[Método GetObject](icordebugthread-getobject-method.md)|Obtém um ponteiro de interface para o thread Common Language Runtime (CLR).|  
|[Método GetProcess](icordebugthread-getprocess-method.md)|Obtém um ponteiro de interface para o processo do qual este `ICorDebugThread` forma uma parte.|  
|[Método GetRegisterSet](icordebugthread-getregisterset-method.md)|Obtém um ponteiro de interface para o conjunto de registros associado a isso `ICorDebugThread` .|  
|[Método GetUserState](icordebugthread-getuserstate-method.md)|Obtém uma combinação de bits de valor CorDebugUserState que descreve o estado atual disso `ICorDebugThread` .|  
|[Método SetDebugState](icordebugthread-setdebugstate-method.md)|Define uma combinação de bits de `CorDebugThreadState` valores que descreve o estado de depuração disso `ICorDebugThread` .|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
