---
description: 'Saiba mais sobre o método: ICorDebugAppDomain3:: GetCachedWinRTTypes'
title: Método ICorDebugAppDomain3::GetCachedWinRTTypes
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3.GetCachedWinRTTypes
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypes
helpviewer_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypes method [.NET Framework debugging]
- GetCachedWinRTTypes method, ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 9afd0e04-a403-41e2-9528-a6dcbcdcbd4d
topic_type:
- apiref
ms.openlocfilehash: 813fb6c05d5e1e5f119424c6e983b86b3ff5889d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772231"
---
# <a name="icordebugappdomain3getcachedwinrttypes-method"></a>Método ICorDebugAppDomain3::GetCachedWinRTTypes

Obtém um enumerador para todos os tipos de Windows Runtime em cache.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCachedWinRTTypes (
    [out] ICorDebugGuidToTypeEnum **ppGuidToTypeEnum)  
;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppGuidToTypeEnum`  
 fora Um ponteiro para um objeto de interface [ICorDebugGuidToTypeEnum](icordebugguidtotypeenum-interface.md) que pode enumerar as representações gerenciadas dos tipos de Windows Runtime atualmente carregados no domínio do aplicativo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** Windows Runtime  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugAppDomain3](icordebugappdomain3-interface.md)
