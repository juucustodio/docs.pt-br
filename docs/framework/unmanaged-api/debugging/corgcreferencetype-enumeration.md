---
description: 'Saiba mais sobre: Enumeração CorGCReferenceType'
title: Enumeração CorGCReferenceType
ms.date: 03/30/2017
api_name:
- CorGCReferenceType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorGCReferenceType
helpviewer_keywords:
- CorGCReferenceType
ms.assetid: d9f16439-5a36-4474-8ffd-4f0b2c2bb686
topic_type:
- apiref
ms.openlocfilehash: a1f534f9fe4b9ba4ede0bef94f35cf1688fe1817
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801508"
---
# <a name="corgcreferencetype-enumeration"></a>Enumeração CorGCReferenceType

Identifica a fonte de um objeto para ser coletado do lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    CorHandleStrong = 1,  
    CorHandleStrongPinning = 2,  
    CorHandleWeakShort = 4,  
    CorHandleWeakRefCount = 8,  
    CorHandleStrongRefCount = 32,  
    CorHandleStrongDependent = 64,  
    CorHandleStrongAsyncPinned = 128,  
    CorHandleStrongSizedByref = 256,  
  
    CorReferenceStack = 0x80000001,  
    CorReferenceFinalizer = 0x80000002,  
  
    CorHandleStrongOnly = 0x1E3,  
    CorHandleWeakOnly = 0xC,  
    CorHandleAll = 0x7FFFFFFF  
} CorGCReferenceType  
```  
  
## <a name="members"></a>Membros  
  
|Nome do membro|Descrição|  
|-----------------|-----------------|  
|`CorHandleStrong`|Uma alça para uma referência forte da tabela de identificador de objeto.|  
|`CorHandleStrongPinning`|Um identificador para uma referência forte fixada da tabela de identificadores de objeto.|  
|`CorHandleWeakShort`|Um identificador para uma referência fraca da tabela de identificadores de objeto.|  
|`CorHandleWeakRefCount`|Um identificador para um objeto de referência fraca contada da tabela de identificadores de objeto.|  
|`CorHandleStrongRefCount`|Um identificador para um objeto de referência contado da tabela de identificadores de objeto.|  
|`CorHandleStrongDependent`|Um identificador para um objeto dependente da tabela de identificadores de objeto.|  
|`CorHandleStrongAsyncPinned`|Um objeto fixo assíncrono da tabela de identificador de objeto.|  
|`CorHandleStrongSizedByref`|Uma alça forte que mantém um tamanho aproximado do fechamento coletivo de todos os objetos e raízes de objeto no momento da coleta de lixo.|  
|`CorReferenceStack`|Uma referência da pilha gerenciada.|  
|`CorReferenceFinalizer`|Uma referência da fila do finalizador.|  
|CorHandleStrongOnly|Retornar apenas referências fortes da tabela de identificadores. Esse valor é usado apenas pelo método [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md) .|  
|`CorHandleWeakOnly`|Retornar apenas referências fracas da tabela de identificadores. Esse valor é usado apenas pelo método [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md) .|  
|`CorHandleAll`|Retorna todas as referências da tabela de identificador. Esse valor é usado apenas pelo método [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md) .|  
  
## <a name="remarks"></a>Comentários  

 A `CorGCReferenceType` enumeração é usada da seguinte maneira:  
  
- Como o valor do `type` campo da estrutura de [COR_GC_REFERENCE](cor-gc-reference-structure.md) , ele indica a origem de uma referência ou um identificador.  
  
- Como o `types` argumento para o método [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md) , ele especifica os tipos de identificadores a serem incluídos na enumeração.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
