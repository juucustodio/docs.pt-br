---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: GetEventMask'
title: Método ICorProfilerInfo::GetEventMask
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetEventMask
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetEventMask
helpviewer_keywords:
- GetEventMask method [.NET Framework profiling]
- ICorProfilerInfo::GetEventMask method [.NET Framework profiling]
ms.assetid: ec34cc13-45a3-4695-abc3-b3347d4e6fc2
topic_type:
- apiref
ms.openlocfilehash: 8ae02a0ef98330207fa7ce6366342d5e0bcb4f19
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647629"
---
# <a name="icorprofilerinfogeteventmask-method"></a>Método ICorProfilerInfo::GetEventMask

Obtém as categorias de eventos atuais para as quais o criador de perfil deseja receber notificações de eventos para o Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetEventMask(  
    [out] DWORD *pdwEvents);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwEvents`  
 [out] Um ponteiro para um valor de 4 bytes que especifica as categorias de eventos. Cada bit controla uma capacidade, um comportamento ou um tipo de evento diferente. Os bits são descritos na enumeração [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) .  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Você deve chamar o método [GetEventMask2](icorprofilerinfo5-geteventmask2-method.md) em vez desse método. Embora o `SetEventMask` método continue a ser suportado, o [GetEventMask2](icorprofilerinfo5-geteventmask2-method.md) fornece funcionalidade adicional.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetEventMask2](icorprofilerinfo5-geteventmask2-method.md)
- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
