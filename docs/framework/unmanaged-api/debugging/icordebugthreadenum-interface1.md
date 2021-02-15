---
description: 'Saiba mais sobre: interface ICorDebugThreadEnum'
title: Interface ICorDebugThreadEnum
ms.date: 03/30/2017
api_name:
- ICorDebugThreadEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThreadEnum
helpviewer_keywords:
- ICorDebugThreadEnum interface [.NET Framework debugging]
ms.assetid: 796de687-7dd4-4b7b-a10b-8bf22dc7779f
topic_type:
- apiref
ms.openlocfilehash: 088b9bd56ae0049ad5f287b07cd2857f70a496c3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658471"
---
# <a name="icordebugthreadenum-interface"></a>Interface ICorDebugThreadEnum

Implementa métodos ICorDebugEnum e enumera matrizes ICorDebugThread.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Next](icordebugthreadenum-next-method.md)|Obtém o número especificado de `ICorDebugThread` instâncias da enumeração, começando na posição atual.|  
  
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
