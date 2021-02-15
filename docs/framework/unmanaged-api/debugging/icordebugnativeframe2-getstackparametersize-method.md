---
description: 'Saiba mais sobre o método: ICorDebugNativeFrame2:: GetStackParameterSize'
title: Método ICorDebugNativeFrame2::GetStackParameterSize
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2.GetStackParameterSize Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2::GetStackParameterSize
helpviewer_keywords:
- ICorDebugNativeFrame2::GetStackParameterSize method [.NET Framework debugging]
- GetStackParameterSize method [.NET Framework debugging]
ms.assetid: f6a449c8-a941-43ba-9a90-c98b29ae3c36
topic_type:
- apiref
ms.openlocfilehash: 08a17ced0be75737c1c49aa3f9bb42b13bbe8aa0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99722302"
---
# <a name="icordebugnativeframe2getstackparametersize-method"></a>Método ICorDebugNativeFrame2::GetStackParameterSize

Retorna o tamanho cumulativo dos parâmetros na pilha em sistemas operacionais x86.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetStackParameterSize([out] ULONG32 * pSize)  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pSize`  
 fora Um ponteiro para o tamanho cumulativo dos parâmetros na pilha.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O tamanho da pilha foi retornado com êxito.|  
|S_FALSE|`GetStackParameterSize` foi chamado em uma plataforma não x86.|  
|E_FAIL|`The size of the parameters could not be returned`.|  
|E_INVALIDARG|`pSize` É `null` .|  
  
## <a name="exceptions"></a>Exceções  
  
## <a name="remarks"></a>Comentários  

 Os métodos [ICorDebugStackWalk](icordebugstackwalk-interface.md) não ajustam o ponteiro de pilha para parâmetros que são enviados por push na pilha. Em vez disso, você pode usar o valor retornado pelo `GetStackParameterSize` para ajustar o ponteiro de pilha para propagar um desenrolador nativo, que se ajusta para os parâmetros.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugNativeFrame2](icordebugnativeframe2-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
