---
description: 'Saiba mais sobre: interface ICorDebugModuleEnum'
title: Interface ICorDebugModuleEnum
ms.date: 03/30/2017
api_name:
- ICorDebugModuleEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModuleEnum
helpviewer_keywords:
- ICorDebugModuleEnum interface [.NET Framework debugging]
ms.assetid: 2fb93cd6-6d47-4fdc-a9a0-047726fd03a1
topic_type:
- apiref
ms.openlocfilehash: c9c847f926984ed2b8aea87463e351cd97a62c80
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801040"
---
# <a name="icordebugmoduleenum-interface"></a>Interface ICorDebugModuleEnum

Implementa métodos ICorDebugEnum e enumera matrizes ICorDebugModule.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Next](icordebugmoduleenum-next-method.md)|Obtém o número especificado de `ICorDebugModule` instâncias da enumeração, começando na posição atual.|  
  
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
