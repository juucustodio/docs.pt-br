---
description: 'Saiba mais sobre o método: ICorDebugProcess:: EnableLogMessages'
title: Método ICorDebugProcess::EnableLogMessages
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.EnableLogMessages
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::EnableLogMessages
helpviewer_keywords:
- ICorDebugProcess::EnableLogMessages method [.NET Framework debugging]
- EnableLogMessages method [.NET Framework debugging]
ms.assetid: 14a4e5a3-3eaf-4f53-9dd1-762726963a23
topic_type:
- apiref
ms.openlocfilehash: d44f1a14611493372c7321feaa14329d5d77b01b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753985"
---
# <a name="icordebugprocessenablelogmessages-method"></a>Método ICorDebugProcess::EnableLogMessages

Habilita e desabilita a transmissão de mensagens de log para o depurador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnableLogMessages([in]BOOL fOnOff);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fOnOff`  
 [in] `true` habilita a transmissão de mensagens de log; `false` desabilita a transmissão.  
  
## <a name="remarks"></a>Comentários  

 Esse método é válido somente depois que o retorno de chamada [ICorDebugManagedCallback:: CreateProcess](icordebugmanagedcallback-createprocess-method.md) ocorre.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
