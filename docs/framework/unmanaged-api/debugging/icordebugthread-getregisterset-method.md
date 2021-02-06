---
description: 'Saiba mais sobre o método: ICorDebugThread:: getregisterset'
title: Método ICorDebugThread::GetRegisterSet
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetRegisterSet
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetRegisterSet
helpviewer_keywords:
- ICorDebugThread::GetRegisterSet method [.NET Framework debugging]
- GetRegisterSet method, ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 3b9b6260-98ac-4cfd-88e5-5d7614f94a0c
topic_type:
- apiref
ms.openlocfilehash: f61ccb34eabc1f4d8b8db8a0b78e3ddde9aa136d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658874"
---
# <a name="icordebugthreadgetregisterset-method"></a>Método ICorDebugThread::GetRegisterSet

Obtém um ponteiro de interface para o conjunto de registros que está associado à parte ativa deste objeto ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRegisterSet (  
    [out] ICorDebugRegisterSet **ppRegisters  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppRegisters`  
 fora Um ponteiro para o endereço de um objeto de interface [ICorDebugRegisterSet](icordebugregisterset-interface.md) que representa o conjunto de registros para a parte ativa desse thread.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
