---
description: 'Saiba mais sobre o método: ICorDebugAppDomain:: Attach'
title: Método ICorDebugAppDomain::Attach
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.Attach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::Attach
helpviewer_keywords:
- ICorDebugAppDomain::Attach method [.NET Framework debugging]
- Attach method [.NET Framework debugging]
ms.assetid: 0358b84a-4236-4c34-945b-4babff7df570
topic_type:
- apiref
ms.openlocfilehash: 94448937a735b30d0403a207992dae29920a93bc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754271"
---
# <a name="icordebugappdomainattach-method"></a>Método ICorDebugAppDomain::Attach

Anexa o depurador ao domínio do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Attach ();  
```  
  
## <a name="remarks"></a>Comentários  

 O depurador deve ser anexado ao domínio do aplicativo para receber eventos e habilitar a depuração do domínio do aplicativo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
