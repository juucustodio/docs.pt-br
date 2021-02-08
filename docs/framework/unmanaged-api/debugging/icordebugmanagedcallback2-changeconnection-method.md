---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback2:: ChangeConnection'
title: Método ICorDebugManagedCallback2::ChangeConnection
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.ChangeConnection
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::ChangeConnection
helpviewer_keywords:
- ICorDebugManagedCallback2::ChangeConnection method [.NET Framework debugging]
- ChangeConnection method [.NET Framework debugging]
ms.assetid: 7263f9a9-4c0b-4d82-a181-288873fb2b18
topic_type:
- apiref
ms.openlocfilehash: 854ea7f40cad9bce613b4034afe7688f4aaf4e52
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790913"
---
# <a name="icordebugmanagedcallback2changeconnection-method"></a>Método ICorDebugManagedCallback2::ChangeConnection

Notifica o depurador de que o conjunto de tarefas associado à conexão especificada foi alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ChangeConnection (  
    [in] ICorDebugProcess     *pProcess,  
    [in] CONNID               dwConnectionId  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pProcess`  
 no Um ponteiro para um objeto "ICorDebugProcess" que representa o processo que contém a conexão que foi alterada.  
  
 `dwConnectionId`  
 no A ID da conexão que foi alterada.  
  
## <a name="remarks"></a>Comentários  

 Um `ChangeConnection` retorno de chamada será acionado em qualquer um dos seguintes casos:  
  
- Quando um depurador é anexado a um processo que contém conexões. Nesse caso, o tempo de execução irá gerar e distribuir um evento [ICorDebugManagedCallback2:: CreateConnection](icordebugmanagedcallback2-createconnection-method.md) e um `ChangeConnection` evento para cada conexão no processo. Um `ChangeConnection` evento é gerado para cada conexão existente, independentemente de o conjunto de tarefas dessa conexão ter sido alterado desde sua criação.  
  
- Quando um host chama [ICLRDebugManager:: SetConnectionTasks](../hosting/iclrdebugmanager-setconnectiontasks-method.md) na [API de hospedagem](../hosting/index.md).  
  
 O depurador deve verificar todos os threads no processo para selecionar as novas alterações.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)
- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
