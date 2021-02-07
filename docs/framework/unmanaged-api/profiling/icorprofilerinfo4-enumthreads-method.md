---
description: 'Saiba mais sobre o método: ICorProfilerInfo4:: EnumThreads'
title: Método ICorProfilerInfo4::EnumThreads
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.EnumThreads
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::EnumThreads
helpviewer_keywords:
- ICorProfilerInfo4::EnumThreads method [.NET Framework profiling]
- EnumThreads method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: bca7a5b4-c207-4894-918c-0733926296dd
topic_type:
- apiref
ms.openlocfilehash: d597e68b8765e135d5bdb403dbdb161b7acbaa9b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686928"
---
# <a name="icorprofilerinfo4enumthreads-method"></a>Método ICorProfilerInfo4::EnumThreads

Retorna um enumerador que fornece métodos para iterar sequencialmente pela coleção de todos os threads gerenciados no processo de perfil.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumThreads([out]  
            ICorProfilerThreadEnum** ppEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppEnum`  
 fora Um ponteiro para uma interface [ICorProfilerThreadEnum](icorprofilerthreadenum-interface.md) .  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerThreadEnum](icorprofilerthreadenum-interface.md)
- [Interface ICorProfilerInfo4](icorprofilerinfo4-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Criação de perfil](index.md)
