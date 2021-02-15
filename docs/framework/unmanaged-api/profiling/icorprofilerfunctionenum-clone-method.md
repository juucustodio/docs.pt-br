---
description: 'Saiba mais sobre o método: ICorProfilerFunctionEnum:: clone'
title: Método ICorProfilerFunctionEnum::Clone
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum.Clone Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum::Clone
helpviewer_keywords:
- ICorProfilerFunctionEnum::Clone method [.NET Framework profiling]
- Clone method, ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 0c3d4835-e111-4e82-af6d-53f140b8f2c9
topic_type:
- apiref
ms.openlocfilehash: 6cadadd98f64a27de0cd4e7d264fe797d22c33a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737662"
---
# <a name="icorprofilerfunctionenumclone-method"></a>Método ICorProfilerFunctionEnum::Clone

Obtém um ponteiro de interface para uma cópia desta interface [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Clone([out] ICorProfilerFunctionEnum **ppEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppEnum`  
 fora Um ponteiro para o ponteiro de interface, que, por sua vez, aponta para a cópia dessa interface [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) . A cópia do enumerador mantém seu próprio estado de enumeração separadamente deste enumerador. No entanto, a posição inicial do cursor da cópia é igual à posição atual do cursor do enumerador.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
