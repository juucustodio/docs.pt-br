---
description: 'Saiba mais sobre: interface ICorDebugRegisterSet2'
title: Interface ICorDebugRegisterSet2
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2
helpviewer_keywords:
- ICorDebugRegisterSet2 interface [.NET Framework debugging]
ms.assetid: d7fbccbf-3b6b-4db8-a96d-768e1cb6b1a6
topic_type:
- apiref
ms.openlocfilehash: 3501325df188879f5687347ef329f490b487d9d8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803601"
---
# <a name="icordebugregisterset2-interface"></a>Interface ICorDebugRegisterSet2

Estende os recursos da interface [ICorDebugRegisterSet](icordebugregisterset-interface.md) para plataformas de hardware que têm mais de 64 registros.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetRegisters](icordebugregisterset2-getregisters-method.md)|Obtém o valor de cada registro (no computador que está executando o código) que é especificado pela máscara de bits.|  
|[Método GetRegistersAvailable](icordebugregisterset2-getregistersavailable-method.md)|Obtém uma matriz de bytes que fornece um bitmap dos registros disponíveis.|  
|[Método SetRegisters](icordebugregisterset2-setregisters-method.md)|Não implementado na versão .NET Framework 2,0.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)
