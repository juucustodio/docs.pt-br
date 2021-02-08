---
description: 'Saiba mais sobre o método: ICorDebugInternalFrame:: GetFrameType'
title: Método ICorDebugInternalFrame::GetFrameType
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame.GetFrameType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame::GetFrameType
helpviewer_keywords:
- GetFrameType method [.NET Framework debugging]
- ICorDebugInternalFrame::GetFrameType method [.NET Framework debugging]
ms.assetid: da278a29-dc2e-4bf7-96ce-801bdc4d7025
topic_type:
- apiref
ms.openlocfilehash: ea96f032ebfa5914503287d124242b74a84ea11f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791173"
---
# <a name="icordebuginternalframegetframetype-method"></a>Método ICorDebugInternalFrame::GetFrameType

Obtém o tipo deste quadro interno.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetFrameType (  
    [out] CorDebugInternalFrameType  *pType  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pType`  
 fora Um ponteiro para um valor da enumeração CorDebugInternalFrameType que indica o tipo de quadro interno representado por esse `ICorDebugInternalFrame` objeto.  
  
## <a name="remarks"></a>Comentários  

 O tipo de quadro interno nunca será STUBFRAME_NONE. Os depuradores devem ignorar normalmente os tipos de quadro internos não reconhecidos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
