---
description: 'Saiba mais sobre o método: ICorDebugAssembly2:: IsFullyTrusted'
title: Método ICorDebugAssembly2::IsFullyTrusted
ms.date: 03/30/2017
api_name:
- ICorDebugAssembly2.IsFullyTrusted
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssembly2::IsFullyTrusted
helpviewer_keywords:
- ICorDebugAssembly2::IsFullyTrusted method [.NET Framework debugging]
- IsFullyTrusted method [.NET Framework debugging]
ms.assetid: 26cbd27d-12bf-444a-8197-ccd14d37dda3
topic_type:
- apiref
ms.openlocfilehash: bc1c4d9a4fa84bac3469aafe8aaa061473e50413
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754102"
---
# <a name="icordebugassembly2isfullytrusted-method"></a>Método ICorDebugAssembly2::IsFullyTrusted

Obtém um valor que indica se o assembly recebeu confiança total pelo sistema de segurança de tempo de execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsFullyTrusted(  
    [out] BOOL *pbFullyTrusted  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbFullyTrusted`  
 [fora] `true` Se o assembly tiver recebido confiança total pelo sistema de segurança de tempo de execução; caso contrário, `false` .  
  
## <a name="remarks"></a>Comentários  

 Esse método retornará um HRESULT de CORDBG_E_NOTREADY se a política de segurança para o assembly ainda não tiver sido resolvida, ou seja, se nenhum código no assembly tiver sido executado ainda.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
