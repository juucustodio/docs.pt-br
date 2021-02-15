---
description: 'Saiba mais sobre o método: ICorProfilerInfo4:: GetFunctionFromIP2'
title: Método ICorProfilerInfo4::GetFunctionFromIP2
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetFunctionFromIP2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetFunctionFromIP2
helpviewer_keywords:
- ICorProfilerInfo4::GetFunctionFromIP2 method [.NET Framework profiling]
- GetFunctionFromIP2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 46ff70f4-13e9-40a0-802a-0a40abcfc6a0
topic_type:
- apiref
ms.openlocfilehash: f6abda7c9e7d4abcc0f0b256d6a7785cea205d7a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686798"
---
# <a name="icorprofilerinfo4getfunctionfromip2-method"></a>Método ICorProfilerInfo4::GetFunctionFromIP2

Mapeia um ponteiro de instrução de código gerenciado para a versão recompilada do JIT de uma função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFunctionFromIP2(  
    [in]  LPCBYTE    ip,  
    [out] FunctionID *pFunctionId,  
    [out] ReJITID *pReJitId);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ip`  
 no O ponteiro de instrução no código gerenciado.  
  
 `pFunctionId`  
 fora A ID da função.  
  
 `pReJitId`  
 fora A identidade da versão recompilada do JIT da função.  
  
## <a name="remarks"></a>Comentários  

 `GetFunctionFromIP2` é semelhante a `GetFunctionFromIP` , exceto pelo fato de que ele obtém a ID recompilada de JIT em vez da ID de função da função que contém o endereço IP especificado.  
  
> [!NOTE]
> `GetFunctionFromIP2` pode disparar uma coleta de lixo, enquanto `GetFunctionFromIP` não vai.  Para obter mais informações, consulte [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
