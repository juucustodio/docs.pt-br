---
description: 'Saiba mais sobre o método: ICorProfilerThreadEnum:: clone'
title: Método ICorProfilerThreadEnum::Clone
ms.date: 03/30/2017
api_name:
- ICorProfilerThreadEnum.Clone
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerThreadEnum::Clone
helpviewer_keywords:
- Clone method, ICorProfilerThreadEnum interface [.NET Framework profiling]
- ICorProfilerThreadEnum::Clone method [.NET Framework profiling]
ms.assetid: 5a278bc9-88e2-4c69-b035-9d550dd77081
topic_type:
- apiref
ms.openlocfilehash: 00920484ed6f089f40281ea2590e6d9c27cd3268
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783788"
---
# <a name="icorprofilerthreadenumclone-method"></a>Método ICorProfilerThreadEnum::Clone

Obtém um ponteiro de interface para uma cópia desta interface [ICorProfilerThreadEnum](icorprofilerthreadenum-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Clone (    [out] ICorProfilerThreadEnum **ppEnum  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppEnum`  
 fora Um ponteiro para o ponteiro de interface, que, por sua vez, aponta para a cópia dessa interface [ICorProfilerThreadEnum](icorprofilerthreadenum-interface.md) . A cópia do enumerador mantém seu próprio estado de enumeração separadamente deste enumerador. No entanto, a posição inicial do cursor da cópia é igual à atual posição do cursor do enumerador.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [ICorProfilerThreadEnum](icorprofilerthreadenum-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
