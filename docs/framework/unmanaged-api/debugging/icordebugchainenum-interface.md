---
description: 'Saiba mais sobre: interface ICorDebugChainEnum'
title: Interface ICorDebugChainEnum
ms.date: 03/30/2017
api_name:
- ICorDebugChainEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChainEnum
helpviewer_keywords:
- ICorDebugChainEnum interface [.NET Framework debugging]
ms.assetid: 6639335c-48e1-4e74-a4f3-70a6a0f54af1
topic_type:
- apiref
ms.openlocfilehash: 948bca1e01a49e7cd2e3fbadca7e3957e5ce38c0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661149"
---
# <a name="icordebugchainenum-interface"></a>Interface ICorDebugChainEnum

Implementa métodos ICorDebugEnum e enumera matrizes ICorDebugChain.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Next](icordebugchainenum-next-method.md)|Obtém o número especificado de `ICorDebugChain` instâncias da enumeração, começando na posição atual.|  
  
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
