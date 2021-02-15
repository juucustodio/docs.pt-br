---
description: 'Saiba mais sobre o método: ICorDebugMutableDataTarget:: SetThreadContext'
title: 'Método ICorDebugMutableDataTarget:: SetThreadContext'
ms.date: 03/30/2017
ms.assetid: 8c0d01d5-67e5-4522-9ccf-c8f3a78cb4fd
ms.openlocfilehash: 4674df92b72b44e19eff663c9a17dd8ca4b5a1b0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99722471"
---
# <a name="icordebugmutabledatatargetsetthreadcontext-method"></a>Método ICorDebugMutableDataTarget:: SetThreadContext

Define o contexto (valores de registro) para um thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetThreadContext(  
   [in] DWORD dwThreadID,  
   [in] ULONG32 contextSize,   [in, size_is(contextSize)] const BYTE * pContext);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwThreadID`  
 no O identificador de thread definido pelo sistema operacional.  
  
 `contextSize`  
 no O tamanho do `pContext` buffer a ser gravado.  
  
 `pContext`  
 no Um ponteiro para os bytes a serem gravados.  
  
## <a name="remarks"></a>Comentários  

 O `SetThreadContext` método atualiza o contexto atual para o thread especificado pelo argumento definido pelo sistema operacional `dwThreadID` . O formato do registro de contexto é determinado pela plataforma indicada pelo método [ICorDebugDataTarget:: GetPlatform](icordebugdatatarget-getplatform-method.md) . No Windows, essa é uma estrutura de [contexto](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugMutableDataTarget](icordebugmutabledatatarget-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
