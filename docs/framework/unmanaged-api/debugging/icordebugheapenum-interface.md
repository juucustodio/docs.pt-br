---
description: 'Saiba mais sobre: interface ICorDebugHeapEnum'
title: Interface ICorDebugHeapEnum
ms.date: 03/30/2017
api_name:
- ICorDebugHeapEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapEnum
helpviewer_keywords:
- ICorDebugHeapEnum interface [.NET Framework debugging]
ms.assetid: 99cbc1eb-d539-4f76-a0d8-b93348112f14
topic_type:
- apiref
ms.openlocfilehash: c8a2f46bf412e2c4b2fe43d3eb50169191f40445
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99660889"
---
# <a name="icordebugheapenum-interface"></a>Interface ICorDebugHeapEnum

Fornece um enumerador para objetos no heap gerenciado. Essa interface é uma subclasse da interface ICorDebugEnum.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Next](icordebugheapenum-next-method.md)|Obtém o número especificado de instâncias de [COR_HEAPOBJECT](cor-heapobject-structure.md) que contêm informações sobre objetos no heap gerenciado.|  
  
## <a name="remarks"></a>Comentários  

 A `ICorDebugHeapEnum` interface implementa a interface ICorDebugEnum.  
  
 Uma `ICorDebugHeapEnum` instância é populada com instâncias de [COR_HEAPOBJECT](cor-heapobject-structure.md) chamando o método [ICorDebugProcess5:: EnumerateHeap](icordebugprocess5-enumerateheap-method.md) . Cada instância de [COR_HEAPOBJECT](cor-heapobject-structure.md) na coleção representa um objeto dinâmico no heap ou um objeto que não tem raiz por nenhum objeto, mas ainda não foi coletado pelo coletor de lixo. Os objetos [COR_HEAPOBJECT](cor-heapobject-structure.md) na coleção podem ser enumerados chamando o método [ICorDebugHeapEnum:: Next](icordebugheapenum-next-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
