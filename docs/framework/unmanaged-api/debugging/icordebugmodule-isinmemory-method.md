---
description: 'Saiba mais sobre o método: ICorDebugModule:: IsInMemory'
title: Método ICorDebugModule::IsInMemory
ms.date: 03/30/2017
api_name:
- ICorDebugModule.IsInMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::IsInMemory
helpviewer_keywords:
- IsInMemory method [.NET Framework debugging]
- ICorDebugModule::IsInMemory method [.NET Framework debugging]
ms.assetid: 89940711-98e7-4aa6-bffc-5e39e91e1b7d
topic_type:
- apiref
ms.openlocfilehash: 41454ede15e1d45775af8fb0ab7a6b571d9c0e41
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99660083"
---
# <a name="icordebugmoduleisinmemory-method"></a>Método ICorDebugModule::IsInMemory

Obtém um valor que indica se esse módulo existe apenas na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsInMemory(  
    [out] BOOL *pInMemory  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pInMemory`  
 [fora] `true` Se esse módulo existir apenas na memória; caso contrário, `false` .  
  
## <a name="remarks"></a>Comentários  

 O Common Language Runtime (CLR) dá suporte ao carregamento de módulos de fluxos brutos de bytes. Esses módulos são chamados *de módulos na memória* e não existem no disco.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Confira também
