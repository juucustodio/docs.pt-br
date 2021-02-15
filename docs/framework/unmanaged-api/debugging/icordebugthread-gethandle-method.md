---
description: 'Saiba mais sobre o método: ICorDebugThread:: GetHandle'
title: Método ICorDebugThread::GetHandle
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetHandle
helpviewer_keywords:
- GetHandle method, ICorDebugThread interface [.NET Framework debugging]
- ICorDebugThread::GetHandle method [.NET Framework debugging]
ms.assetid: 172ef8c4-2ead-4cfc-bd2e-dee4fb7191cd
topic_type:
- apiref
ms.openlocfilehash: 378bb395e56f0fc287a480d67d2047e082d0796f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659095"
---
# <a name="icordebugthreadgethandle-method"></a>Método ICorDebugThread::GetHandle

Obtém o identificador atual da parte ativa deste ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetHandle (  
    [out] HTHREAD *phThreadHandle  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phThreadHandle`  
 fora Um ponteiro para um HTHREAD que é o identificador da parte ativa deste thread.  
  
## <a name="remarks"></a>Comentários  

 O identificador pode ser alterado conforme o processo é executado e pode ser diferente para partes diferentes do thread.  
  
 Esse identificador é de propriedade da API de depuração. O depurador deve duplicá-lo antes de usá-lo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
