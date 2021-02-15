---
description: 'Saiba mais sobre o método: ICorDebugProcess:: ModifyLogSwitch'
title: Método ICorDebugProcess::ModifyLogSwitch
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ModifyLogSwitch
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ModifyLogSwitch
helpviewer_keywords:
- ICorDebugProcess::ModifyLogSwitch method [.NET Framework debugging]
- ModifyLogSwitch method [.NET Framework debugging]
ms.assetid: 5fd30875-555e-4e96-877b-5dd266cde7c4
topic_type:
- apiref
ms.openlocfilehash: 3c825d6c6b075139793b54526dca696c8fba35a4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746749"
---
# <a name="icordebugprocessmodifylogswitch-method"></a>Método ICorDebugProcess::ModifyLogSwitch

Define o nível de severidade da opção de log especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ModifyLogSwitch(  
    [in] WCHAR *pLogSwitchName,  
    [in] LONG  lLevel);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pLogSwitchName`  
 no Um ponteiro para uma cadeia de caracteres que especifica o nome do comutador de log.  
  
 `lLevel`  
 no O nível de severidade a ser definido para o comutador de log especificado.  
  
## <a name="remarks"></a>Comentários  

 Este método é válido somente depois que o retorno de chamada [ICorDebugManagedCallback:: CreateProcess](icordebugmanagedcallback-createprocess-method.md) ocorreu.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
