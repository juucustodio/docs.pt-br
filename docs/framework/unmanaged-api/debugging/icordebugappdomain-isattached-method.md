---
description: 'Saiba mais sobre: método ICorDebugAppDomain:: isanexou'
title: Método ICorDebugAppDomain::IsAttached
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.IsAttached
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::IsAttached
helpviewer_keywords:
- IsAttached method [.NET Framework debugging]
- ICorDebugAppDomain::IsAttached method [.NET Framework debugging]
ms.assetid: af0c67c7-f53e-47c9-b84b-be50bd04903e
topic_type:
- apiref
ms.openlocfilehash: 79427d08be9ffea253695b67767d68589edf6979
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772374"
---
# <a name="icordebugappdomainisattached-method"></a>Método ICorDebugAppDomain::IsAttached

Obtém um valor que indica se o depurador está anexado ao domínio do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsAttached (  
    [out] BOOL  *pbAttached  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbAttached`  
 [fora] `true` Se o depurador estiver anexado ao domínio do aplicativo; caso contrário, `false` .  
  
## <a name="remarks"></a>Comentários  

 Os métodos ICorDebugController não podem ser usados até que o depurador seja anexado ao domínio do aplicativo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
