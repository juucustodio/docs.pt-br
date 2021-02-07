---
description: 'Saiba mais sobre o método: ICorDebugComObjectValue:: GetCachedInterfaceTypes'
title: Método ICorDebugComObjectValue::GetCachedInterfaceTypes
ms.date: 03/30/2017
api_name:
- ICorDebugComObjectValue::GetCachedInterfaceTypes
api_location:
- mscordbi.dll
f1_keywords:
- ICorDebugComObjectValue::GetCachedInterfaceTypes
helpviewer_keywords:
- GetCachedInterface method, ICorDebugComObjectValue interface [.NET Framework debugging]
- ICorDebugComObjectValue::GetCachedInterface method [.NET Framework debugging]
ms.assetid: d492284f-d3c5-4614-adb8-d718d5042500
topic_type:
- apiref
ms.openlocfilehash: b1c65979895dfaeacae3d171adbcfd1455b7030d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764613"
---
# <a name="icordebugcomobjectvaluegetcachedinterfacetypes-method"></a>Método ICorDebugComObjectValue::GetCachedInterfaceTypes

Fornece um enumerador para os tipos de interface para os quais o objeto atual foi convertido ou usado como.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCachedInterfaceTypes(  
    [in] BOOL bIInspectableOnly,  
    [out] ICorDebugTypeEnum **ppInterfacesEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `bIInspectableOnly`  
 no Um valor que indica se o método retorna apenas interfaces Windows Runtime ( `IInspectable` interfaces) ou todas as interfaces com armazenadas em cache pelo RCW (Runtime Callable Wrapper).  
  
 `ppInterfacesEnum`  
 fora Um ponteiro para o endereço de um enumerador ICorDebugTypeEnum que fornece acesso a objetos ICorDebugType que representam tipos de interface em cache filtrados de acordo com `bIInspectableOnly` .  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugComObjectValue](icordebugcomobjectvalue-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
