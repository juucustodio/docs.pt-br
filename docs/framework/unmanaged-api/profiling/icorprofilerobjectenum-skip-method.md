---
description: 'Saiba mais sobre o método: ICorProfilerObjectEnum:: Skip'
title: Método ICorProfilerObjectEnum::Skip
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum.Skip
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum::Skip
helpviewer_keywords:
- ICorProfilerObjectEnum::Skip method [.NET Framework profiling]
- Skip method, ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: f8e498f8-f93a-4b82-bd22-55bdbf5e8d45
topic_type:
- apiref
ms.openlocfilehash: 8a2aa5dd2b905931b97fafa4db6709aab16aacc4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781253"
---
# <a name="icorprofilerobjectenumskip-method"></a>Método ICorProfilerObjectEnum::Skip

Avança o cursor deste enumerador de sua posição atual para que o número especificado de elementos seja ignorado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Skip (  
    [in] ULONG   celt  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 no O número de elementos a serem ignorados.  
  
## <a name="remarks"></a>Comentários  

 A nova posição do cursor deste enumerador é: (posição atual) + `celt` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerObjectEnum](icorprofilerobjectenum-interface.md)
