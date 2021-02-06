---
description: 'Saiba mais sobre o método: ICorDebugThread:: GetActiveFrame'
title: Método ICorDebugThread::GetActiveFrame
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetActiveFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetActiveFrame
helpviewer_keywords:
- ICorDebugThread::GetActiveFrame method [.NET Framework debugging]
- GetActiveFrame method, ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 8d6d3a1a-fef6-4f2f-a22c-3bdd30d70e07
topic_type:
- apiref
ms.openlocfilehash: 3b15aad39503dfec9ac8f98f839ee1a6b16b3f90
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659251"
---
# <a name="icordebugthreadgetactiveframe-method"></a>Método ICorDebugThread::GetActiveFrame

Obtém um ponteiro de interface para o quadro ativo (mais recente) neste objeto ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetActiveFrame (  
    [out] ICorDebugFrame   **ppFrame  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppFrame`  
 fora Um ponteiro para o endereço de um objeto de interface ICorDebugFrame que representa um quadro.  
  
## <a name="remarks"></a>Comentários  

 O `ppFrame` parâmetro será NULL se nenhum quadro estiver ativo no momento.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
