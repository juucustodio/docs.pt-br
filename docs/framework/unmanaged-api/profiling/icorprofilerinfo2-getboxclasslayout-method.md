---
description: 'Saiba mais sobre o método: ICorProfilerInfo2:: GetBoxClassLayout'
title: Método ICorProfilerInfo2::GetBoxClassLayout
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetBoxClassLayout
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetBoxClassLayout
helpviewer_keywords:
- GetBoxClassLayout method [.NET Framework profiling]
- ICorProfilerInfo2::GetBoxClassLayout method [.NET Framework profiling]
ms.assetid: 624672b5-1189-488a-85d2-3e12b49617c1
topic_type:
- apiref
ms.openlocfilehash: 0bc9ccc80da8bcc89cfe73eaa240310c01e6ca8f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760464"
---
# <a name="icorprofilerinfo2getboxclasslayout-method"></a>Método ICorProfilerInfo2::GetBoxClassLayout

Obtém informações sobre onde o tipo de valor especificado está localizado quando ele está em caixa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetBoxClassLayout(  
    [in] ClassID classId,  
    [out] ULONG32 *pBufferOffset);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `classId`  
 no A ID da classe que descreve o tipo de valor que está em caixa.  
  
 `pBufferOffset`  
 fora Um inteiro que é o deslocamento, relativo ao ponteiro da ID do objeto em caixa, do tipo de valor.  
  
## <a name="remarks"></a>Comentários  

 O `pBufferOffset` valor é o local do tipo de valor dentro de uma caixa. Depois `pBufferOffset` que é aplicado a um objeto em caixa, o layout de classe do tipo de valor pode ser usado para interpretar o valor do objeto.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Interface ICorProfilerInfo2](icorprofilerinfo2-interface.md)
