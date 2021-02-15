---
description: 'Saiba mais sobre o método: ICorDebugInternalFrame2:: IsCloserToLeaf'
title: Método ICorDebugInternalFrame2::IsCloserToLeaf
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame2.IsCloserToLeaf Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf
helpviewer_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf method [.NET Framework debugging]
- IsCloserToLeaf method [.NET Framework debugging]
ms.assetid: c1d3d1eb-8370-4f25-8297-3bd262b4740a
topic_type:
- apiref
ms.openlocfilehash: d773f8670f600a5bcd2a8dad7f23fe243195957c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801274"
---
# <a name="icordebuginternalframe2isclosertoleaf-method"></a>Método ICorDebugInternalFrame2::IsCloserToLeaf

Verifica se o `this` quadro interno está mais próximo da folha do que o objeto ICorDebugFrame especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsCloserToLeaf([in] ICorDebugFrame * pFrameToCompare,  
                       [out] BOOL * pIsCloser);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pFrameToCompare`  
 no Um ponteiro para o objeto de comparação `ICorDebugFrame` .  
  
 `pIsCloser`  
 [fora] `true` Se o `this` quadro interno estiver mais próximo da folha do que o quadro especificado por `pFrameToCompare` ; caso contrário, `false` .  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A comparação foi executada com êxito.|  
|E_FAIL|Não foi possível executar a comparação.|  
|E_INVALIDARG|`pFrameToCompare` ou `pIsCloser` é nulo.|  
  
## <a name="remarks"></a>Comentários  

 `IsCloserToLeaf` pode ser usado para implementar uma política para intercalar quadros internos com outros quadros na pilha.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugInternalFrame2](icordebuginternalframe2-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
