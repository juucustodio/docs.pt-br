---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: SetILFunctionBody'
title: Método ICorProfilerInfo::SetILFunctionBody
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetILFunctionBody
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetILFunctionBody
helpviewer_keywords:
- ICorProfilerInfo::SetILFunctionBody method [.NET Framework profiling]
- SetILFunctionBody method [.NET Framework profiling]
ms.assetid: b159c712-00f4-4fc7-a990-40bf9f642e8f
topic_type:
- apiref
ms.openlocfilehash: 38e7907080065dc96d72a3d38a67227414637a70
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647161"
---
# <a name="icorprofilerinfosetilfunctionbody-method"></a>Método ICorProfilerInfo::SetILFunctionBody

Substitui o corpo da função especificada no módulo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetILFunctionBody(  
    [in] ModuleID    moduleId,  
    [in] mdMethodDef methodid,  
    [in] LPCBYTE     pbNewILMethodHeader);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `moduleId`  
 no A ID do módulo no qual a função reside.  
  
 `methodid`  
 no O token da função para a qual substituir o corpo.  
  
 `pbNewILMethodHeader`  
 no O novo cabeçalho da função.  
  
## <a name="remarks"></a>Comentários  

 O `SetILFunctionBody` método substitui o endereço virtual relativo da função nos metadados para que ele aponte para o novo corpo da função e ajusta todas as estruturas de dados internas conforme necessário.  
  
 O `SetILFunctionBody` método pode ser chamado somente nas funções que nunca foram compiladas por um compilador JIT (just-in-time).  
  
 Use o método [ICorProfilerInfo:: GetILFunctionBodyAllocator](icorprofilerinfo-getilfunctionbodyallocator-method.md) para alocar espaço para o novo método a fim de garantir que o buffer seja compatível.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
