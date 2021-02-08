---
description: 'Saiba mais sobre: estrutura de COR_HEAPOBJECT'
title: Estrutura COR_HEAPOBJECT
ms.date: 03/30/2017
api_name:
- COR_HEAPOBJECT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_HEAPOBJECT
helpviewer_keywords:
- COR_HEAPOBJECT structure [.NET Framework debugging]
ms.assetid: a92fdf95-492b-49ae-a741-2186e5c1d7c5
topic_type:
- apiref
ms.openlocfilehash: f41e02e7c528063f4b7ed485cbadbabb4d3e5ca7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801794"
---
# <a name="cor_heapobject-structure"></a>Estrutura COR_HEAPOBJECT

Fornece informações sobre um objeto no heap gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _COR_HEAPOBJECT {  
    CORDB_ADDRESS address;
    ULONG64 size;
    COR_TYPEID type;
} COR_HEAPOBJECT;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`address`|O endereço do objeto na memória.|  
|`size`|O tamanho total do objeto, em bytes.|  
|`type`|Um [COR_TYPEID](cor-typeid-structure.md) token que representa o tipo do objeto.|  
  
## <a name="remarks"></a>Comentários  

 `COR_HEAPOBJECT` as instâncias podem ser recuperadas enumerando um objeto de interface [ICorDebugHeapEnum](icordebugheapenum-interface.md) que é populado chamando o método [ICorDebugProcess5:: EnumerateHeap](icordebugprocess5-enumerateheap-method.md) .  
  
 Uma `COR_HEAPOBJECT` instância do fornece informações sobre um objeto ao vivo no heap gerenciado ou sobre um objeto que não tem raiz por nenhum objeto, mas que ainda não foi coletado pelo coletor de lixo.  
  
 Para obter um melhor desempenho, o `COR_HEAPOBJECT.address` campo é um `CORDB_ADDRESS` valor em vez do valor da interface ICorDebugValue usado em grande parte da API de depuração. Para obter um objeto ICorDebugValue para um determinado endereço de objeto, você pode passar o `CORDB_ADDRESS` valor para o método [ICorDebugProcess5:: GetObject](icordebugprocess5-getobject-method.md) .  
  
 Para obter um melhor desempenho, o `COR_HEAPOBJECT.type` campo é um `COR_TYPEID` valor em vez do valor da interface ICorDebugType usado em grande parte da API de depuração. Para obter um objeto ICorDebugType para uma determinada ID de tipo, você pode passar o `COR_TYPEID` valor para o método [ICorDebugProcess5:: GetTypeForTypeID](icordebugprocess5-gettypefortypeid-method.md) .  
  
 A `COR_HEAPOBJECT` estrutura inclui uma interface com contada com referência. Se você recuperar uma `COR_HEAPOBJECT` instância do enumerador chamando o método [ICorDebugHeapEnum:: Next](icordebugheapenum-next-method.md) , você deverá liberar a referência posteriormente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
