---
description: 'Saiba mais sobre: método ICorDebugModule:: IsDynamic'
title: Método ICorDebugModule::IsDynamic
ms.date: 03/30/2017
api_name:
- ICorDebugModule.IsDynamic
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::IsDynamic
helpviewer_keywords:
- IsDynamic method [.NET Framework debugging]
- ICorDebugModule::IsDynamic method [.NET Framework debugging]
ms.assetid: 5eefe716-5025-4a4c-970c-c823cdc7bb87
topic_type:
- apiref
ms.openlocfilehash: 06ecb7aaffbe73da29bbdbba9446839db54c58c3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99660096"
---
# <a name="icordebugmoduleisdynamic-method"></a>Método ICorDebugModule::IsDynamic

Obtém um valor que indica se este módulo é dinâmico.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsDynamic(  
    [out] BOOL *pDynamic  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pDynamic`  
 [fora] `true` Se esse módulo for dinâmico; caso contrário, `false` .  
  
## <a name="remarks"></a>Comentários  

 Um módulo dinâmico pode adicionar novas classes e excluir classes existentes mesmo depois que o módulo tiver sido carregado. Os retornos de chamada [ICorDebugManagedCallback:: LoadClass](icordebugmanagedcallback-loadclass-method.md) e [ICorDebugManagedCallback:: UnloadClass](icordebugmanagedcallback-unloadclass-method.md) informam ao depurador quando uma classe foi adicionada ou excluída.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
