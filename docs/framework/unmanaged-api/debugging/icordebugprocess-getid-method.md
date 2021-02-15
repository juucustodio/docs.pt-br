---
description: 'Saiba mais sobre o método: ICorDebugProcess:: GetID'
title: Método ICorDebugProcess::GetID
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetID
helpviewer_keywords:
- GetID method, ICorDebugProcess interface [.NET Framework debugging]
- ICorDebugProcess::GetID method [.NET Framework debugging]
ms.assetid: b0ba8453-fa7e-4c14-93e5-335409cd4a47
topic_type:
- apiref
ms.openlocfilehash: 806e73724a88d08235f4a3e751f771abace1ad56
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746978"
---
# <a name="icordebugprocessgetid-method"></a>Método ICorDebugProcess::GetID

Obtém a ID do sistema operacional (SO) do processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetID([out] DWORD *pdwProcessId);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwProcessId`  
 fora A ID exclusiva do processo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
