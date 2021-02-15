---
description: 'Saiba mais sobre: método ICorDebug:: Terminate'
title: Método ICorDebug::Terminate
ms.date: 03/30/2017
api_name:
- ICorDebug.Terminate
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::Terminate
helpviewer_keywords:
- Terminate method, ICorDebug interface [.NET Framework debugging]
- ICorDebug::Terminate method [.NET Framework debugging]
ms.assetid: fffe5616-0896-4426-ab5e-21869b514883
topic_type:
- apiref
ms.openlocfilehash: c2de27a47bfd4c364a09180c75109679234f3cae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754284"
---
# <a name="icordebugterminate-method"></a>Método ICorDebug::Terminate

Encerra o `ICorDebug` objeto.  
  
> [!NOTE]
> `Terminate` Não deve ser chamado até que um retorno de chamada [ICorDebugManagedCallback:: ExitProcess](icordebugmanagedcallback-exitprocess-method.md) tenha sido recebido para todos os processos sendo depurados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Terminate ();  
```  
  
## <a name="remarks"></a>Comentários  

 `Terminate` deve ser chamado quando o `ICorDebug` objeto não for mais necessário.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebug](icordebug-interface.md)
