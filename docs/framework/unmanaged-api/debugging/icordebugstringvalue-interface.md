---
description: 'Saiba mais sobre: interface ICorDebugStringValue'
title: Interface ICorDebugStringValue
ms.date: 03/30/2017
api_name:
- ICorDebugStringValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStringValue
helpviewer_keywords:
- ICorDebugStringValue interface [.NET Framework debugging]
ms.assetid: bf84d0af-53e1-4c04-bc5b-7e5f81ba2cc2
topic_type:
- apiref
ms.openlocfilehash: b4e762d8c0a62c1b76b59364e9d29c4b8d2386fa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717323"
---
# <a name="icordebugstringvalue-interface"></a>Interface ICorDebugStringValue

Uma subclasse de ICorDebugHeapValue que se aplica a valores de cadeia de caracteres.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetLength](icordebugstringvalue-getlength-method.md)|Obtém o número de caracteres na cadeia de caracteres referenciada por isso `ICorDebugStringValue` .|  
|[Método GetString](icordebugstringvalue-getstring-method.md)|Obtém a cadeia de caracteres referenciada por isso `ICorDebugStringValue` .|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
