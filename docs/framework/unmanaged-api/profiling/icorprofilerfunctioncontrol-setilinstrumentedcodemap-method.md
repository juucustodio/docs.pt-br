---
description: 'Saiba mais sobre o método: ICorProfilerFunctionControl:: SetILInstrumentedCodeMap'
title: Método ICorProfilerFunctionControl::SetILInstrumentedCodeMap
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl.SetILInstrumentedCodeMap
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl::SetILInstrumentedCodeMap
helpviewer_keywords:
- ICorProfilerFunctionControl::SetILInstrumentedCodeMap method [.NET Framework profiling]
- SetIILInstrumentedCodeMap method, ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: ecf56646-7e5f-46c4-8340-f3a04e88920f
topic_type:
- apiref
ms.openlocfilehash: bb345f737459342e0146cbb0e0bd7dd4b1e9a037
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781539"
---
# <a name="icorprofilerfunctioncontrolsetilinstrumentedcodemap-method"></a>Método ICorProfilerFunctionControl::SetILInstrumentedCodeMap

Define um mapa de códigos para a função especificada usando as entradas de mapa Common Intermediate Language (CIL) especificadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetILInstrumentedCodeMap(  
    [in]   ULONG      cILMapEntries,  
    [in, size_is(cILMapEntries)] COR_IL_MAP rgILMapEntries[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cILMapEntries`  
 [in] O número de entradas no mapa.  
  
 `rgILMapEntries`  
 [in] A matriz alocada pelo chamador de entradas COR_IL_MAP. A interpretação dessas entradas é a mesma do método [ICorProfilerInfo:: SetILInstrumentedCodeMap](icorprofilerinfo-setilinstrumentedcodemap-method.md) .  
  
## <a name="remarks"></a>Comentários  

 Definir o mapeamento chamando esse método permite que o depurador recupere o mapeamento chamando [ICorDebugILCode2:: GetInstrumentedILMap](../debugging/icordebugilcode2-getinstrumentedilmap-method.md). Ele permite também que o depurador use o mapeamento internamente ao calcular deslocamentos de IL para rastreamentos de pilha e tempos de vida variáveis.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
