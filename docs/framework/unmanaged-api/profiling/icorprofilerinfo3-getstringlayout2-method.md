---
description: 'Saiba mais sobre o método: ICorProfilerInfo3:: GetStringLayout2'
title: Método ICorProfilerInfo3::GetStringLayout2
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetStringLayout2 Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetStringLayout2
helpviewer_keywords:
- ICorProfilerInfo3::GetStringLayout2 method [.NET Framework profiling]
- GetStringLayout2 method [.NET Framework profiling]
ms.assetid: 1a268496-ee51-4d84-8700-ee56fd0c499d
topic_type:
- apiref
ms.openlocfilehash: 398d06dc62245e6a2201feacb62ebbb1e4839ccb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646667"
---
# <a name="icorprofilerinfo3getstringlayout2-method"></a>Método ICorProfilerInfo3::GetStringLayout2

Obtém informações sobre o layout de um objeto de cadeia de caracteres. Esse método substitui o método [ICorProfilerInfo2:: GetStringLayout](icorprofilerinfo2-getstringlayout-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetStringLayout2(  
    [out] ULONG *pStringLengthOffset,  
    [out] ULONG *pBufferOffset);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pStringLengthOffset`  
 fora Um ponteiro para o deslocamento do local, relativo ao `ObjectID` ponteiro, que armazena o comprimento da própria cadeia de caracteres. O comprimento é armazenado como um `DWORD` .  
  
 `pBufferOffset`  
 fora Um ponteiro para o deslocamento do buffer, relativo ao `ObjectID` ponteiro, que armazena a cadeia de caracteres largos.  
  
## <a name="remarks"></a>Comentários  

 Cadeias de caracteres podem ou não ser terminadas em nulo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo3](icorprofilerinfo3-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
