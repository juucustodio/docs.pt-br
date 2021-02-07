---
description: 'Saiba mais sobre o método: ICorDebugCode:: GetFunction'
title: Método ICorDebugCode::GetFunction
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetFunction
helpviewer_keywords:
- GetFunction method, ICorDebugCode interface [.NET Framework debugging]
- ICorDebugCode::GetFunction method [.NET Framework debugging]
ms.assetid: c568b737-fdb2-4816-accd-051f5ab760f1
topic_type:
- apiref
ms.openlocfilehash: c90635bf1821d70d6d056d5cbd495ddfa2d2a2ff
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99711200"
---
# <a name="icordebugcodegetfunction-method"></a>Método ICorDebugCode::GetFunction

Obtém o "ICorDebugFunction" associado a este "ICorDebugCode".  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFunction (  
    [out] ICorDebugFunction **ppFunction  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppFunction`  
 fora Um ponteiro para o endereço da função.  
  
## <a name="remarks"></a>Comentários  

 `ICorDebugCode` e `ICorDebugFunction` manter uma relação um-para-um.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
