---
description: 'Saiba mais sobre o método: ICorDebugProcess2:: ClearUnmanagedBreakpoint'
title: Método ICorDebugProcess2::ClearUnmanagedBreakpoint
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.ClearUnmanagedBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::ClearUnmanagedBreakpoint
helpviewer_keywords:
- ClearUnmanagedBreakpoint method [.NET Framework debugging]
- ICorDebugProcess2::ClearUnmanagedBreakpoint method [.NET Framework debugging]
ms.assetid: 12ed0fff-7f0e-4d7a-bb70-b3376371f36c
topic_type:
- apiref
ms.openlocfilehash: fba31a479e9bac525109e14c02995e78918d4c17
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746617"
---
# <a name="icordebugprocess2clearunmanagedbreakpoint-method"></a>Método ICorDebugProcess2::ClearUnmanagedBreakpoint

Remove um ponto de interrupção definido anteriormente no endereço fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ClearUnmanagedBreakpoint (  
    [in] CORDB_ADDRESS   address  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `address`  
 no Um `CORDB_ADDRESS` valor que especifica o endereço no qual o ponto de interrupção foi definido.  
  
## <a name="remarks"></a>Comentários  

 O ponto de interrupção especificado teria sido definido anteriormente por uma chamada anterior para [ICorDebugProcess2:: SetUnmanagedBreakpoint](icordebugprocess2-setunmanagedbreakpoint-method.md).  
  
 O `ClearUnmanagedBreakpoint` método pode ser chamado enquanto o processo que está sendo depurado está em execução.  
  
 O `ClearUnmanagedBreakpoint` método retornará um código de falha se o depurador estiver anexado no modo somente gerenciado ou se não existir nenhum ponto de interrupção no endereço especificado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
