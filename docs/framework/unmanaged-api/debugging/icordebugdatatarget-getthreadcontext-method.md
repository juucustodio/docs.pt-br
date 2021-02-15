---
description: 'Saiba mais sobre o método: ICorDebugDataTarget:: GetThreadContext'
title: Método ICorDebugDataTarget::GetThreadContext
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget.GetThreadContext Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget::GetThreadContext
helpviewer_keywords:
- ICorDebugDataTarget::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: c8954268-1821-4b23-b665-dbb55f2af31b
topic_type:
- apiref
ms.openlocfilehash: cf40579aa0a495af4e5e775334d177ca6f3da86f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710628"
---
# <a name="icordebugdatatargetgetthreadcontext-method"></a>Método ICorDebugDataTarget::GetThreadContext

Retorna o contexto do thread atual para o thread especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetThreadContext(  
       [in] DWORD dwThreadID,  
       [in] ULONG32 contextFlags,  
       [in] ULONG32 contextSize,  
       [out, size_is(contextSize)] BYTE * pContext);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwThreadID`  
 no O identificador do thread cujo contexto deve ser recuperado. O identificador é definido pelo sistema operacional.  
  
 `contextFlags`  
 no Uma combinação de bits e de sinalizadores que dependem de plataforma que indicam quais partes do contexto devem ser lidas.  
  
 `contextSize`  
 [in] O tamanho do `pContext`.  
  
 `pContext`  
 fora O buffer em que o contexto de thread será armazenado.  
  
## <a name="remarks"></a>Comentários  

 Em plataformas Windows, `pContext` deve ser uma `CONTEXT` estrutura (definida em Winnt. h) apropriada para o tipo de computador especificado pelo método [ICorDebugDataTarget:: GetPlatform](icordebugdatatarget-getplatform-method.md) . `contextFlags` deve ter os mesmos valores que o `ContextFlags` campo da `CONTEXT` estrutura. A `CONTEXT` estrutura é específica do processador; consulte o arquivo Winnt. h para obter detalhes.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugDataTarget](icordebugdatatarget-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
