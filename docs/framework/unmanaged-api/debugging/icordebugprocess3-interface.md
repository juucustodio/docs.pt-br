---
description: 'Saiba mais sobre: interface ICorDebugProcess3'
title: Interface ICorDebugProcess3
ms.date: 03/30/2017
api_name:
- ICorDebugProcess3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess3
helpviewer_keywords:
- ICorDebugProcess3 interface [.NET Framework debugging]
ms.assetid: ced9c82e-d7b0-4806-a151-98b6611d3097
topic_type:
- apiref
ms.openlocfilehash: 28b588bb4718f841e78b89ce44821971800b1f6f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649969"
---
# <a name="icordebugprocess3-interface"></a>Interface ICorDebugProcess3

Controla as notificações personalizadas do depurador.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método SetEnableCustomNotification](icordebugprocess3-setenablecustomnotification-method.md)|Habilita e desabilita as notificações do depurador personalizado do tipo especificado.|  
  
## <a name="remarks"></a>Comentários  

 Essa interface estende logicamente as interfaces ICorDebugProcess e ICorDebugProcess2.  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
