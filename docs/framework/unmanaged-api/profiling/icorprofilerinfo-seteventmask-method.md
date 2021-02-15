---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: SetEventMask'
title: Método ICorProfilerInfo::SetEventMask
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetEventMask
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetEventMask
helpviewer_keywords:
- ICorProfilerInfo::SetEventMask method [.NET Framework profiling]
- SetEventMask method [.NET Framework profiling]
ms.assetid: 44bc0f56-32fa-491e-a62d-52fc96d48125
topic_type:
- apiref
ms.openlocfilehash: e389d25abfecfc9a5dec8834e412fe618324e311
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99687188"
---
# <a name="icorprofilerinfoseteventmask-method"></a>Método ICorProfilerInfo::SetEventMask

Determina um valor que especifica os tipos de eventos dos quais o perfil deseja receber notificação do CLR (Common Language Runtime).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetEventMask(  
    [in] DWORD dwEvents);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwEvents`  
 [in] Um valor de 4 bytes que especifica as categorias de eventos. Cada bit controla uma capacidade, um comportamento ou um tipo de evento diferente. Os bits são descritos na enumeração [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) .  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Você deve chamar o método [SetEventMask2](icorprofilerinfo5-seteventmask2-method.md) em vez desse método. Embora o `SetEventMask` método continue a ser suportado, o [SetEventMask2](icorprofilerinfo5-seteventmask2-method.md) fornece funcionalidade adicional.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Método SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)
