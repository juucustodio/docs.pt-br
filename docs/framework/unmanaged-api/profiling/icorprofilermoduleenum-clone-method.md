---
description: 'Saiba mais sobre o método: ICorProfilerModuleEnum:: clone'
title: Método ICorProfilerModuleEnum::Clone
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum.Clone Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum::Clone
helpviewer_keywords:
- Clone method, ICorProfilerModuleEnum interface [.NET Framework profiling]
- ICorProfilerModuleEnum::Clone method [.NET Framework profiling]
ms.assetid: 7dec7e36-8d88-416d-b437-abf98b76c1df
topic_type:
- apiref
ms.openlocfilehash: 0d2a235def6d3b16d661e51979742426ebe1942f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99736928"
---
# <a name="icorprofilermoduleenumclone-method"></a>Método ICorProfilerModuleEnum::Clone

Obtém um ponteiro de interface para uma cópia desta interface [ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Clone([out] ICorProfilerObjectEnum **ppEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppEnum`  
 fora Um ponteiro para o ponteiro de interface que, por sua vez, aponta para a cópia dessa interface [ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md) . A cópia do enumerador mantém seu próprio estado de enumeração separadamente deste enumerador. No entanto, a posição inicial do cursor da cópia é igual à posição atual do cursor do enumerador.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
