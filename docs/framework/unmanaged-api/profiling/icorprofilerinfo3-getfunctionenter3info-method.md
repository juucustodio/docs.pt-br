---
description: 'Saiba mais sobre o método: ICorProfilerInfo3:: GetFunctionEnter3Info'
title: Método ICorProfilerInfo3::GetFunctionEnter3Info
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetFunctionEnter3Info Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetFunctionEnter3Info
helpviewer_keywords:
- GetFunctionEnter3Info method [.NET Framework profiling]
- ICorProfilerInfo3::GetFunctionEnter3Info method [.NET Framework profiling]
ms.assetid: 542c7c65-dd56-4651-b76f-5db2465e4a15
topic_type:
- apiref
ms.openlocfilehash: 3e6c0cfbf2518301e62ed5c57e956190066504ba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646810"
---
# <a name="icorprofilerinfo3getfunctionenter3info-method"></a>Método ICorProfilerInfo3::GetFunctionEnter3Info

Fornece o quadro de pilha e as informações de argumento da função que está sendo relatada para o criador de perfil pela função [FunctionEnter3WithInfo](functionenter3withinfo-function.md) . Esse método pode ser chamado somente durante o `FunctionEnter3WithInfo` retorno de chamada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFunctionEnter3Info(  
            [in]  FunctionID functionId,
            [in]  COR_PRF_ELT_INFO eltInfo,  
            [out] COR_PRF_FRAME_INFO *pFrameInfo,  
            [in, out] ULONG *pcbArgumentInfo,  
            [out, size_is(*pcbArgumentInfo)]  
                  COR_PRF_FUNCTION_ARGUMENT_INFO *pArgumentInfo);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `functionId`  
 no A `FunctionID` da função que está sendo inserida.  
  
 `eltInfo`  
 no Um identificador opaco que representa informações sobre um determinado registro de ativação. O criador de perfil deve fornecer o mesmo `eltInfo` que foi fornecido pela função [FunctionEnter3WithInfo](functionenter3withinfo-function.md) .  
  
 `pFrameInfo`  
 fora Um identificador opaco que representa informações genéricas sobre um determinado registro de ativação. Esse identificador é válido somente durante o `FunctionEnter3WithInfo` retorno de chamada no qual o criador de perfil chamou o `GetFunctionEnter3Info` método.  
  
 `pcbArgumentInfo`  
 [entrada, saída] Um ponteiro para o tamanho total, em bytes, da estrutura de [COR_PRF_FUNCTION_ARGUMENT_INFO](cor-prf-function-argument-info-structure.md) (mais quaisquer estruturas de [COR_PRF_FUNCTION_ARGUMENT_RANGE](cor-prf-function-argument-range-structure.md) adicionais para os intervalos de argumento apontados por `pArgumentInfo` ). Se o tamanho especificado não for suficiente, ERROR_INSUFFICIENT_BUFFER será retornado e o tamanho esperado será armazenado em `pcbArgumentInfo` . Para chamar `GetFunctionEnter3Info` apenas para recuperar o valor esperado para `*pcbArgumentInfo` , defina `*pcbArgumentInfo` = 0 e `pArgumentInfo` = NULL.  
  
 `pArgumentInfo`  
 fora Um ponteiro para uma estrutura de [COR_PRF_FUNCTION_ARGUMENT_INFO](cor-prf-function-argument-info-structure.md) que descreve os locais dos argumentos da função na memória, na ordem da esquerda para a direita.  
  
## <a name="remarks"></a>Comentários  

 O criador de perfil deve alocar espaço suficiente para a `COR_PRF_FUNCTION_ARGUMENT_INFO` estrutura da função que está sendo inspecionada e deve indicar o tamanho no `pcbArgumentInfo` parâmetro.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [Interface ICorProfilerInfo3](icorprofilerinfo3-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Criação de perfil](index.md)
