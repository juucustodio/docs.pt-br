---
description: 'Saiba mais sobre o método: ICorDebugFunction2:: GetJMCStatus'
title: Método ICorDebugFunction2::GetJMCStatus
ms.date: 03/30/2017
api_name:
- ICorDebugFunction2.GetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction2::GetJMCStatus
helpviewer_keywords:
- ICorDebugFunction2::GetJMCStatus method [.NET Framework debugging]
- GetJMCStatus method [.NET Framework debugging]
ms.assetid: 840a71ed-bf5a-4f5e-8ed6-762222b34493
topic_type:
- apiref
ms.openlocfilehash: 42c72256df57b96a52737f4a0e5e90d6ba5d4e0c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692284"
---
# <a name="icordebugfunction2getjmcstatus-method"></a>Método ICorDebugFunction2::GetJMCStatus

Obtém um valor que indica se a função representada por esse objeto ICorDebugFunction2 está marcada como código de usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetJMCStatus (  
    [out] BOOL   *pbIsJustMyCode  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbIsJustMyCode`  
 fora Um ponteiro para um valor booliano `true` , se essa função estiver marcada como código de usuário; caso contrário, o valor será `false` .  
  
## <a name="remarks"></a>Comentários  

 Se a função representada por isso `ICorDebugFunction2` não puder ser depurada, `pbIsJustMyCode` sempre será `false` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
