---
description: 'Saiba mais sobre: interface ICorDebugAppDomainEnum'
title: Interface ICorDebugAppDomainEnum
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomainEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomainEnum
helpviewer_keywords:
- ICorDebugAppDomainEnum interface [.NET Framework debugging]
ms.assetid: e9226e6e-ca2c-428e-bb38-0c099210f507
topic_type:
- apiref
ms.openlocfilehash: dfea6254e6cf4f162e44d057fb4126a67a087b61
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754149"
---
# <a name="icordebugappdomainenum-interface"></a>Interface ICorDebugAppDomainEnum

Fornece o `Next` método, que retorna um número especificado de `ICorDebugAppDomainEnum` valores começando no próximo local na enumeração. Essa interface é uma subclasse de "ICorDebugEnum".  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Next](icordebugappdomainenum-next-method.md)|Obtém o número especificado de domínios de aplicativo da coleção, começando na posição atual do cursor.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebug](icordebug-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
