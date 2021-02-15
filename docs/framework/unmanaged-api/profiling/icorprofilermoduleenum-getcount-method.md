---
description: 'Saiba mais sobre o método: ICorProfilerModuleEnum:: GetCount'
title: Método ICorProfilerModuleEnum::GetCount
ms.date: 03/30/2017
api_name:
- ICorProfilerModuleEnum.GetCount Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerModuleEnum::GetCount
helpviewer_keywords:
- ICorProfilerModuleEnum::GetCount method [.NET Framework profiling]
- GetCount method, ICorProfilerModuleEnum interface [.NET Framework profiling]
ms.assetid: f0a4a5e0-4689-474b-b0f4-37ca0639c918
topic_type:
- apiref
ms.openlocfilehash: efdd812795002c25aaeb7634e7a4f4e4287553e8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781383"
---
# <a name="icorprofilermoduleenumgetcount-method"></a>Método ICorProfilerModuleEnum::GetCount

Obtém o número de módulos gerenciados que foram carregados no aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCount([out] ULONG * pcelt);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `celt`  
 fora O número de módulos de tempo de execução na coleção.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerModuleEnum](icorprofilermoduleenum-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
