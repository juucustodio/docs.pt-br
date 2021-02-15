---
description: 'Saiba mais sobre o método: ICorDebugChain:: GetCallee'
title: Método ICorDebugChain::GetCallee
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetCallee
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetCallee method
helpviewer_keywords:
- ICorDebugChain::GetCallee method [.NET Framework debugging]
- GetCallee method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: 19560c79-abdc-4bdf-a5fe-eb362a59edc0
topic_type:
- apiref
ms.openlocfilehash: 4787893c86804c648dae14bf2e6f7425808104b7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99661383"
---
# <a name="icordebugchaingetcallee-method"></a>Método ICorDebugChain::GetCallee

Obtém a cadeia que foi chamada por essa cadeia.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCallee (  
    [out] ICorDebugChain     **ppChain  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppChain`  
 fora Um ponteiro para o endereço de um objeto ICorDebugChain que representa a cadeia chamada. Se essa cadeia estiver em execução no momento (ou seja, se essa cadeia não estiver aguardando que uma cadeia chamada retorne), `ppChain` será NULL.  
  
## <a name="remarks"></a>Comentários  

 Essa cadeia aguardará que a cadeia chamada seja retornada antes de retomar a execução. A cadeia chamada pode estar em outro thread no caso de chamadas empacotadas entre threads.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
