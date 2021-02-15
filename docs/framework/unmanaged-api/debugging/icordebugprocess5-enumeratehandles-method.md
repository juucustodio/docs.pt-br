---
description: 'Saiba mais sobre o método: ICorDebugProcess5:: EnumerateHandles'
title: Método ICorDebugProcess5::EnumerateHandles
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHandles
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHandles
helpviewer_keywords:
- EnumerateHandles method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHandles method [.NET Framework debugging]
ms.assetid: 7d7fa796-0dc6-4ee8-9d56-40166246d91d
topic_type:
- apiref
ms.openlocfilehash: 62ca1390ceec634e6651dc013345688fe5892bcd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649904"
---
# <a name="icordebugprocess5enumeratehandles-method"></a>Método ICorDebugProcess5::EnumerateHandles

Obtém um enumerador para identificadores de objeto em um processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateHandles(     [in] CorGCReferenceType types,  
    [out] ICorDebugGCReferenceEnum **ppEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `types`  
 no Uma combinação bits de valores [CorGCReferenceType](corgcreferencetype-enumeration.md) que especifica o tipo de identificadores a serem incluídos na coleção.  
  
 `ppENum`  
 fora Um ponteiro para o endereço de um [ICorDebugGCReferenceEnum](icordebuggcreferenceenum-interface.md) que é um enumerador para os objetos a serem coletados como lixo.  
  
## <a name="remarks"></a>Comentários  

 `EnumerateHandles` é uma função auxiliar que dá suporte à inspeção da tabela de identificadores. Ele é semelhante ao método [ICorDebugProcess5:: EnumerateGCReferences](icordebugprocess5-enumerategcreferences-method.md) , exceto que, em vez de preencher uma coleção [ICorDebugGCReferenceEnum](icordebuggcreferenceenum-interface.md) com todos os objetos a serem coletados pelo lixo, ele inclui somente objetos que têm identificadores da tabela de identificadores.  
  
 O `types` parâmetro especifica os tipos de identificador a serem incluídos na coleção. `types` pode ser qualquer um dos três membros a seguir da enumeração [CorGCReferenceType](corgcreferencetype-enumeration.md) :  
  
- `CorHandleStrongOnly` (lida apenas com referências fortes).  
  
- `CorHandleWeakOnly` (lida apenas com referências fracas).  
  
- `CorHandleAll` (todos os identificadores).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
