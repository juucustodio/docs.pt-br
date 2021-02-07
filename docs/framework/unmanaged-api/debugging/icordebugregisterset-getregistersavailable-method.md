---
description: 'Saiba mais sobre o método: ICorDebugRegisterSet:: GetRegistersAvailable'
title: Método ICorDebugRegisterSet::GetRegistersAvailable
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet.GetRegistersAvailable
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet::GetRegistersAvailable
helpviewer_keywords:
- ICorDebugRegisterSet::GetRegistersAvailable method [.NET Framework debugging]
- GetRegistersAvailable method, ICorDebugRegisterSet interface [.NET Framework debugging]
ms.assetid: 4ba08ffa-55a2-4662-9d6d-4738f1db60c9
topic_type:
- apiref
ms.openlocfilehash: a1727c594733fe6529fe1e78f341723623b68be2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690815"
---
# <a name="icordebugregistersetgetregistersavailable-method"></a>Método ICorDebugRegisterSet::GetRegistersAvailable

Obtém uma máscara de bits que indica quais registros neste [ICorDebugRegisterSet](icordebugregisterset-interface.md) estão disponíveis no momento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRegistersAvailable (  
    [out] ULONG64   *pAvailable  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pAvailable`  
 fora Uma máscara de bits que indica quais registros estão disponíveis no momento.  
  
## <a name="remarks"></a>Comentários  

 Um registro pode não estar disponível se seu valor não puder ser determinado para a situação especificada.  
  
 A máscara retornada contém um bit para cada registro (1 << o índice de registro). O valor de bit será 1 se o registro estiver disponível ou 0 se não estiver disponível.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)
- [Interface ICorDebugRegisterSet2](icordebugregisterset2-interface.md)
