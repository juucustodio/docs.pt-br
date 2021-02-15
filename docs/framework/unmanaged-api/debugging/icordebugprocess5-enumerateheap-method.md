---
description: 'Saiba mais sobre o método: ICorDebugProcess5:: EnumerateHeap'
title: Método ICorDebugProcess5::EnumerateHeap
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeap
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeap
helpviewer_keywords:
- EnumerateHeap method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeap method [.NET Framework debugging]
ms.assetid: b0192104-6073-4089-a4df-dc29ee033074
topic_type:
- apiref
ms.openlocfilehash: b43e7993b114ed64d009f91746ea987198edde74
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99722029"
---
# <a name="icordebugprocess5enumerateheap-method"></a>Método ICorDebugProcess5::EnumerateHeap

Obtém um enumerador para os objetos no heap gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateHeap(  
    [out] ICorDebugHeapEnum **ppObjects  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppObject`  
 fora Um ponteiro para o endereço de um objeto de interface [ICorDebugHeapEnum](icordebugheapenum-interface.md) que é um enumerador para os objetos que residem no heap gerenciado.  
  
## <a name="remarks"></a>Comentários  

 Antes de chamar o `ICorDebugProcess5::EnumerateHeap` método, você deve chamar o método [ICorDebugProcess5:: GetGCHeapInformation](icordebugprocess5-getgcheapinformation-method.md) e examinar o valor do `areGCStructuresValid` campo do objeto de [COR_HEAPINFO](cor-heapinfo-structure.md) retornado para garantir que o heap de coleta de lixo em seu estado atual seja enumerável. Além disso, o `ICorDebugProcess5::EnumerateHeap` retorna `E_FAIL` se você anexar muito cedo no tempo de vida do processo, antes que a memória para o heap gerenciado seja alocada.  
  
 O objeto de interface [ICorDebugHeapEnum](icordebugheapenum-interface.md) é um enumerador padrão derivado da interface ICorDebugEnum que permite que você enumere [COR_HEAPOBJECT](cor-heapobject-structure.md) objetos. Esse método popula o objeto da coleção [ICorDebugHeapEnum](icordebugheapenum-interface.md) com [COR_HEAPOBJECT](cor-heapobject-structure.md) instâncias que fornecem informações sobre todos os objetos. A coleção também pode incluir [COR_HEAPOBJECT](cor-heapobject-structure.md) instâncias que fornecem informações sobre objetos que não são enraizada por nenhum objeto, mas que ainda não foram coletados pelo coletor de lixo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugProcess5](icordebugprocess5-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
