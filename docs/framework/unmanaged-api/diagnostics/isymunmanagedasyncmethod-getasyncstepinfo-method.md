---
description: 'Saiba mais sobre o método: ISymUnmanagedAsyncMethod:: GetAsyncStepInfo'
title: Método ISymUnmanagedAsyncMethod::GetAsyncStepInfo
ms.date: 03/30/2017
ms.assetid: 3ef5b4b8-4ac7-4906-849b-f932c5e3db07
ms.openlocfilehash: dc255323f103b3422b927b0489402b24767dcd92
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737838"
---
# <a name="isymunmanagedasyncmethodgetasyncstepinfo-method"></a>Método ISymUnmanagedAsyncMethod::GetAsyncStepInfo

Consulte o [método DefineAsyncStepInfo](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```idl  
HRESULT GetAsyncStepInfo(    [in] ULONG32 cStepInfo,    [out] ULONG32 *pcStepInfo,    [in, size_is(cStepInfo)] ULONG32 yieldOffsets[],    [in, size_is(cStepInfo)] ULONG32 breakpointOffset[],    [in, size_is(cStepInfo)] mdToken breakpointMethod[]);  
```  
  
## <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`cStepInfo`||  
|`pcStepInfo`||  
|`yieldOffsets`||  
|`breakpointOffset`||  
|`breakpointMethod`||  
  
## <a name="return-value"></a>Valor retornado  

 Retorna `HRESULT`.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedAsyncMethod](isymunmanagedasyncmethod-interface.md)
