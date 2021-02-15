---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: GetILToNativeMapping'
title: Método ICorProfilerInfo::GetILToNativeMapping
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetILToNativeMapping
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetILToNativeMapping
helpviewer_keywords:
- GetILToNativeMapping method, ICorProfilerInfo interface [.NET Framework profiling]
- ICorProfilerInfo::GetILToNativeMapping method [.NET Framework profiling]
ms.assetid: 6a5431ef-22fb-4e53-bac5-703986297eb1
topic_type:
- apiref
ms.openlocfilehash: ce3473365eb98beca4d2e9116251200d7539e4c9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647382"
---
# <a name="icorprofilerinfogetiltonativemapping-method"></a>Método ICorProfilerInfo::GetILToNativeMapping

Obtém um mapa de deslocamentos de MSIL (Microsoft Intermediate Language) para deslocamentos nativos do código contido na função especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetILToNativeMapping(  
    [in] FunctionID functionId,  
    [in] ULONG32 cMap,  
    [out] ULONG32 *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `functionId`  
 no A ID da função que contém o código.  
  
 `cMap`  
 no O tamanho máximo da `map` matriz.  
  
 `pcMap`  
 fora O número total de estruturas de COR_DEBUG_IL_TO_NATIVE_MAP disponíveis.  
  
 `map`  
 fora Uma matriz de `COR_DEBUG_IL_TO_NATIVE_MAP` estruturas, cada uma delas especifica os deslocamentos. Depois que o `GetILToNativeMapping` método retornar, `map` conterá algumas ou todas as `COR_DEBUG_IL_TO_NATIVE_MAP` estruturas.  
  
## <a name="remarks"></a>Comentários  

 O `GetILToNativeMapping` método retorna uma matriz de `COR_DEBUG_IL_TO_NATIVE_MAP` estruturas. Para transmitir que determinados intervalos de instruções nativas correspondem a regiões especiais de código (por exemplo, o prólogo), uma entrada na matriz pode ter seu `ilOffset` campo definido como um valor da enumeração [CorDebugIlToNativeMappingTypes](../debugging/cordebugiltonativemappingtypes-enumeration.md) .  
  
 Depois de `GetILToNativeMapping` retornar, você deve verificar se o `map` buffer foi grande o suficiente para conter todas as `COR_DEBUG_IL_TO_NATIVE_MAP` estruturas. Para fazer isso, compare o valor de `cMap` com o valor do `pcMap` parâmetro. Se o `pcMap` valor, quando for multiplicado pelo tamanho de uma `COR_DEBUG_IL_TO_NATIVE_MAP` estrutura, for maior do que `cMap` , aloque um buffer maior `map` , atualize `cMap` com o novo tamanho, maior e chame `GetILToNativeMapping` novamente.  
  
 Como alternativa, você pode primeiro chamar `GetILToNativeMapping` com um buffer de comprimento zero `map` para obter o tamanho de buffer correto. Em seguida, você pode definir o tamanho do buffer para o valor retornado em `pcMap` e chamar `GetILToNativeMapping` novamente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Método GetILToNativeMapping2](icorprofilerinfo4-getiltonativemapping2-method.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Criação de perfil](index.md)
