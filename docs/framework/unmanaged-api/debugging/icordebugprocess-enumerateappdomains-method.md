---
description: 'Saiba mais sobre o método: ICorDebugProcess:: EnumerateAppDomains'
title: Método ICorDebugProcess::EnumerateAppDomains
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.EnumerateAppDomains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::EnumerateAppDomains
helpviewer_keywords:
- ICorDebugProcess::EnumerateAppDomains method [.NET Framework debugging]
- EnumerateAppDomains method [.NET Framework debugging]
ms.assetid: d508981f-e2b2-445b-a649-69951c22702d
topic_type:
- apiref
ms.openlocfilehash: d212fafe7ae1355ba69e07b88c3b96119371fe43
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99691517"
---
# <a name="icordebugprocessenumerateappdomains-method"></a>Método ICorDebugProcess::EnumerateAppDomains

Enumera todos os domínios de aplicativo neste processo.  
  
## <a name="syntax"></a>Sintaxe  
  
``` cpp
HRESULT EnumerateAppDomains(  
    [out] ICorDebugAppDomainEnum **ppAppDomains);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppAppDomains`  
 fora Um ponteiro para o endereço de um [ICorDebugAppDomainEnum](icordebugappdomainenum-interface.md) que é um enumerador para os domínios de aplicativo nesse processo.  
  
## <a name="remarks"></a>Comentários  

 Esse método pode ser usado antes do retorno de chamada [ICorDebugManagedCallback:: CreateProcess](icordebugmanagedcallback-createprocess-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
