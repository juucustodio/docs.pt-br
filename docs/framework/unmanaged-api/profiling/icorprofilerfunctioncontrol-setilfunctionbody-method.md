---
description: 'Saiba mais sobre o método: ICorProfilerFunctionControl:: SetILFunctionBody'
title: Método ICorProfilerFunctionControl::SetILFunctionBody
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl.SetILFunctionBody
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl::SetILFunctionBody
helpviewer_keywords:
- ICorProfilerFunctionControl::SetILFunctionBody method [.NET Framework profiling]
- SetILFunctionBody method, ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 2c33f0f7-75b2-4c19-b2c7-c94b54997576
topic_type:
- apiref
ms.openlocfilehash: 470eefce5b211adcfd111951be9a004b3bd7d8fc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781604"
---
# <a name="icorprofilerfunctioncontrolsetilfunctionbody-method"></a>Método ICorProfilerFunctionControl::SetILFunctionBody

Substitui o corpo CIL (Common Intermediate Language) do método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetILFunctionBody(  
    [in]  ULONG   cbNewILMethodHeader,  
    [in, size_is(cbNewILMethodHeader)] LPCBYTE pbNewILMethodHeader);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cbNewILMethodHeader`  
 [in] O tamanho total do novo CIL, incluindo o cabeçalho e quaisquer estruturas que vierem após o corpo.  
  
 `pbNewILMethodHeader`  
 [in] Um ponteiro para o novo cabeçalho CIL.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A substituição foi bem-sucedida.|  
  
## <a name="remarks"></a>Comentários  

 Ao contrário do método [ICorProfilerInfo:: SetILFunctionBody](icorprofilerinfo-setilfunctionbody-method.md) , o `SetILFunctionBody` método gerencia a memória necessária para o novo corpo cil. Isso significa que o corpo de CIL fornecido pelo criador de perfil não precisa ser alocado usando a interface [IMethodMalloc](imethodmalloc-interface.md) ou alocado em um intervalo específico. Ele pode ser alocado em qualquer heap. O criador de perfil pode liberar a memória usada para o corpo de CIL após o `SetILFunctionBody` retorno.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerFunctionControl](icorprofilerfunctioncontrol-interface.md)
