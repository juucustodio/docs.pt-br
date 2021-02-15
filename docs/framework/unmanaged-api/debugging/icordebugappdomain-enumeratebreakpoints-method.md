---
description: 'Saiba mais sobre o método: ICorDebugAppDomain:: EnumerateBreakpoints'
title: Método ICorDebugAppDomain::EnumerateBreakpoints
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.EnumerateBreakpoints
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::EnumerateBreakpoints
helpviewer_keywords:
- ICorDebugAppDomain::EnumerateBreakpoints method [.NET Framework debugging]
- EnumerateBreakpoints method [.NET Framework debugging]
ms.assetid: 206069c5-25cb-4794-9d69-67c5aa7ed0af
topic_type:
- apiref
ms.openlocfilehash: 4bd9857b9c662bc76c7c9481f306b20e823e446f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772452"
---
# <a name="icordebugappdomainenumeratebreakpoints-method"></a>Método ICorDebugAppDomain::EnumerateBreakpoints

Obtém um enumerador para todos os pontos de interrupção ativos no domínio do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateBreakpoints (  
    [out] ICorDebugBreakpointEnum   **ppBreakpoints  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppBreakpoints`  
 fora Um ponteiro para o endereço de um objeto ICorDebugBreakpointEnum que é o enumerador para todos os pontos de interrupção ativos no domínio do aplicativo.  
  
## <a name="remarks"></a>Comentários  

 O enumerador inclui todos os tipos de pontos de interrupção, incluindo pontos de interrupção de função e pontos de interrupção de dados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
