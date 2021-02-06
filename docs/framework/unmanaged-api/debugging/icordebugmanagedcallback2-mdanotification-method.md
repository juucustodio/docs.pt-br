---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback2:: MDANotification'
title: Método ICorDebugManagedCallback2::MDANotification
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.MDANotification
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::MDANotification
helpviewer_keywords:
- MDANotification method [.NET Framework debugging]
- ICorDebugManagedCallback2::MDANotification method [.NET Framework debugging]
ms.assetid: 93f79627-bd31-4f4f-b95d-46a032a52fe4
topic_type:
- apiref
ms.openlocfilehash: 3f0c69c13ec30e604e07c284adca05f86283a5cd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650489"
---
# <a name="icordebugmanagedcallback2mdanotification-method"></a>Método ICorDebugManagedCallback2::MDANotification

Fornece uma notificação de que a execução de código encontrou um MDA (Assistente de depuração gerenciada) no aplicativo que está sendo depurado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT MDANotification(  
    [in] ICorDebugController  *pController,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugMDA         *pMDA  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pController`  
 no Um ponteiro para uma interface ICorDebugController que expõe o domínio do processo ou do aplicativo no qual o MDA ocorreu.  
  
 Um depurador não deve fazer suposições sobre se o controlador é um processo ou um domínio de aplicativo, embora ele sempre possa consultar a interface para fazer uma determinação.  
  
 `pThread`  
 no Um ponteiro para uma interface ICorDebugThread que expõe o thread gerenciado no qual o evento de depuração ocorreu.  
  
 Se o MDA ocorreu em um thread não gerenciado, o valor de `pThread` será NULL.  
  
 Você deve obter a ID do thread do sistema operacional (SO) do próprio objeto MDA.  
  
 `pMDA`  
 no Um ponteiro para uma interface [ICorDebugMDA](icordebugmda-interface.md) que expõe as informações de MDA.  
  
## <a name="remarks"></a>Comentários  

 Um MDA é um aviso heurístico e não requer nenhuma ação de depurador explícita, exceto para chamar [ICorDebugController:: Continue](icordebugcontroller-continue-method.md) para retomar a execução do aplicativo que está sendo depurado.  
  
 O Common Language Runtime (CLR) pode determinar quais MDAs são disparadas e quais dados estão em qualquer MDA determinado em qualquer ponto. Portanto, os depuradores não devem criar nenhuma funcionalidade que exija padrões de MDA específicos.  
  
 O MDAs pode ser enfileirado e disparado logo após o MDA ser encontrado. Isso pode acontecer se o tempo de execução precisar esperar até chegar a um ponto seguro para acionar o MDA, em vez de acionar o MDA quando ele encontrá-lo. Isso também significa que o tempo de execução pode disparar vários MDAs em um único conjunto de retornos de chamada em fila (semelhante a uma operação de evento "Attach").  
  
 Um depurador deve liberar a referência a uma `ICorDebugMDA` instância imediatamente após retornar do `MDANotification` retorno de chamada, para permitir que o CLR Recicle a memória consumida por um MDA. A liberação da instância pode melhorar o desempenho se muitas MDAs estiverem sendo acionadas.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Diagnosticando erros com assistentes de depuração gerenciados](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [Interface ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)
- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
