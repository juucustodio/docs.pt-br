---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ObjectsAllocatedByClass'
title: Método ICorProfilerCallback::ObjectsAllocatedByClass
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectsAllocatedByClass
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectsAllocatedByClass
helpviewer_keywords:
- ObjectsAllocatedByClass method [.NET Framework profiling]
- ICorProfilerCallback::ObjectsAllocatedByClass method [.NET Framework profiling]
ms.assetid: 91d688f3-a80e-419d-9755-ff94bc04188a
topic_type:
- apiref
ms.openlocfilehash: df9f3dde27664de7db4afb264b221f640753ddb3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745054"
---
# <a name="icorprofilercallbackobjectsallocatedbyclass-method"></a>Método ICorProfilerCallback::ObjectsAllocatedByClass

Notifica o criador de perfil sobre o número de instâncias de cada classe especificada que foram criadas desde a coleta de lixo mais recente.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ObjectsAllocatedByClass(  
    [in] ULONG   cClassCount,  
    [in, size_is(cClassCount)] ClassID classIds[] ,  
    [in, size_is(cClassCount)] ULONG   cObjects[] );  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cClassCount`  
 no O tamanho das `classIds` `cObjects` matrizes e.  
  
 `classIds`  
 no Uma matriz de IDs de classe, em que cada ID especifica uma classe com uma ou mais instâncias.  
  
 `cObjects`  
 no Uma matriz de inteiros, em que cada inteiro especifica o número de instâncias para a classe correspondente na `classIds` matriz.  
  
## <a name="remarks"></a>Comentários  

 As `classIds` `cObjects` matrizes e são matrizes paralelas. Por exemplo, `classIds[i]` e `cObjects[i]` referenciar a mesma classe. Se nenhuma instância de uma classe tiver sido criada desde a coleta de lixo anterior, a classe será omitida. O `ObjectsAllocatedByClass` retorno de chamada não relatará objetos alocados na heap de objeto grande.  
  
 Os números relatados por `ObjectsAllocatedByClass` são apenas estimativas. Para contagens exatas, use [ICorProfilerCallback:: ObjectAllocated](icorprofilercallback-objectallocated-method.md).  
  
 A `classIds` matriz pode conter uma ou mais entradas nulas se a `cObjects` matriz correspondente tiver tipos que estão descarregando.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
