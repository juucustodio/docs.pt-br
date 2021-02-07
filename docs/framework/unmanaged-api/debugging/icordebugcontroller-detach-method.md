---
description: 'Saiba mais sobre: ICorDebugController: método Etach de:D'
title: Método ICorDebugController::Detach
ms.date: 03/30/2017
api_name:
- ICorDebugController.Detach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Detach
helpviewer_keywords:
- Detach method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Detach method [.NET Framework debugging]
ms.assetid: 06fae364-f2c6-4a50-aa7e-3da9f2684dc3
topic_type:
- apiref
ms.openlocfilehash: 763386fa72fab023becf4a360556e61d500c7949
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764629"
---
# <a name="icordebugcontrollerdetach-method"></a>Método ICorDebugController::Detach

Desanexa o depurador do domínio do processo ou do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Detach ();  
```  
  
## <a name="remarks"></a>Comentários  

 O processo ou o domínio do aplicativo continua a execução normalmente, mas o objeto "ICorDebugProcess" ou "ICorDebugAppDomain" não é mais válido e não ocorrerão nenhum retorno de chamada adicional.  
  
 No .NET Framework versão 2,0, se a depuração não gerenciada estiver habilitada, esse método falhará devido a limitações do sistema operacional.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Confira também
