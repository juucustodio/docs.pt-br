---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ObjectAllocated'
title: Método ICorProfilerCallback::ObjectAllocated
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectAllocated
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectAllocated
helpviewer_keywords:
- ObjectAllocated method [.NET Framework profiling]
- ICorProfilerCallback::ObjectAllocated method [.NET Framework profiling]
ms.assetid: eb412622-77cc-4abd-a2cd-c910fe8edd54
topic_type:
- apiref
ms.openlocfilehash: 58b58aeb4bb88d0df32cebc32440317a4d23632d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745158"
---
# <a name="icorprofilercallbackobjectallocated-method"></a>Método ICorProfilerCallback::ObjectAllocated

Notifica o criador de perfil de que a memória dentro do heap foi alocada para um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ObjectAllocated(  
    [in] ObjectID objectId,  
    [in] ClassID classId);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `objectId`  
 no A ID do objeto para o qual a memória foi alocada.  
  
 `classId`  
 no A ID da classe da qual o objeto é uma instância.  
  
## <a name="remarks"></a>Comentários  

 O `ObjectedAllocated` método não é chamado para alocações a partir da pilha ou da memória não gerenciada. O `classId` parâmetro pode se referir a uma classe no código gerenciado que ainda não foi carregado. O criador de perfil receberá um retorno de chamada de carga de classe para essa classe imediatamente após o `ObjectAllocated` retorno de chamada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método ClassLoadStarted](icorprofilercallback-classloadstarted-method.md)
- [Método ClassLoadFinished](icorprofilercallback-classloadfinished-method.md)
