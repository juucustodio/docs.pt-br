---
description: 'Saiba mais sobre o método: ICorDebugRegisterSet:: GetThreadContext'
title: Método ICorDebugRegisterSet::GetThreadContext
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet.GetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet::GetThreadContext
helpviewer_keywords:
- GetThreadContext method, ICorDebugRegisterSet interface [.NET Framework debugging]
- ICorDebugRegisterSet::GetThreadContext method [.NET Framework debugging]
ms.assetid: 0f63400b-dc1c-48d6-b51a-75c3f7f28e03
topic_type:
- apiref
ms.openlocfilehash: be6384562858d04b6e139eda83c172c09f2dfc0d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99690789"
---
# <a name="icordebugregistersetgetthreadcontext-method"></a>Método ICorDebugRegisterSet::GetThreadContext

Obtém o contexto do thread atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThreadContext(  
    [in] ULONG32 contextSize,  
    [in, out, length_is(contextSize),  
        size_is(contextSize)] BYTE context[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `contextSize`  
 no O tamanho, em bytes, da `context` matriz.  
  
 `context`  
 [entrada, saída] Uma matriz de bytes que compõe a estrutura do Win32 `CONTEXT` para a plataforma atual.  
  
## <a name="remarks"></a>Comentários  

 O depurador deve chamar essa função em vez da função do Win32 `GetThreadContext` , pois o thread pode estar em um estado "seqüestrado" em que seu contexto foi alterado temporariamente. Os dados retornados são uma `CONTEXT` estrutura Win32 para a plataforma atual.  
  
 Para quadros não folha, os clientes devem verificar quais registros são válidos usando [ICorDebugRegisterSet:: GetRegistersAvailable](icordebugregisterset-getregistersavailable-method.md).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)
- [Interface ICorDebugRegisterSet2](icordebugregisterset2-interface.md)
