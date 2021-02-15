---
description: 'Saiba mais sobre o método: ICorDebugRegisterSet2:: setregistras'
title: Método ICorDebugRegisterSet2::SetRegisters
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2.SetRegisters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2::SetRegisters
helpviewer_keywords:
- ICorDebugRegisterSet2::SetRegisters method [.NET Framework debugging]
- SetRegisters method, ICorDebugRegisterSet2 interface [.NET Framework debugging]
ms.assetid: fe0ac7e7-c9e1-4ec1-9f4e-1c56d63d73ac
topic_type:
- apiref
ms.openlocfilehash: d58717be34e146def2a54bb49d6cd58dde7564c8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794748"
---
# <a name="icordebugregisterset2setregisters-method"></a>Método ICorDebugRegisterSet2::SetRegisters

`SetRegisters` Não está implementado na versão .NET Framework 2,0. Não chame esse método.  
  
> [!NOTE]
> Use as operações de nível superior, como [ICorDebugILFrame:: SetIP](icordebugilframe-setip-method.md) ou [ICorDebugNativeFrame:: SetIP](icordebugnativeframe-setip-method.md).  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT SetRegisters (  
    [in] ULONG32 maskCount,  
    [in, size_is(maskCount)] BYTE mask[],  
    [in] ULONG32 regCount,  
    [in, size_is(regCount)] CORDB_REGISTER regBuffer[]  
);  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRegisterSet2](icordebugregisterset2-interface.md)
- [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)
