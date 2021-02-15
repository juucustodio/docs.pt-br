---
description: 'Saiba mais sobre: ICorDebugChain:: método IsManaged'
title: Método ICorDebugChain::IsManaged
ms.date: 03/30/2017
api_name:
- ICorDebugChain.IsManaged
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::IsManaged
helpviewer_keywords:
- ICorDebugChain::IsManaged method [.NET Framework debugging]
- IsManaged method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: 17b389a0-1a4d-4e8a-8613-9bc1769930f9
topic_type:
- apiref
ms.openlocfilehash: 200b76350d474645a40f8ee35859c2db5420ea0a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99694846"
---
# <a name="icordebugchainismanaged-method"></a>Método ICorDebugChain::IsManaged

Obtém um valor que indica se esta cadeia está executando código gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsManaged (  
    [out] BOOL               *pManaged  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pManaged`  
 [fora] `true` Se essa cadeia estiver executando código gerenciado; caso contrário, `false` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
