---
description: 'Saiba mais sobre: ICorDebugILFrame:: método CanSetIP'
title: Método ICorDebugILFrame::CanSetIP
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.CanSetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::CanSetIP
helpviewer_keywords:
- CanSetIP method, ICorDebugILFrame interface [.NET Framework debugging]
- ICorDebugILFrame::CanSetIP method [.NET Framework debugging]
ms.assetid: 16caf02f-c71e-486c-90b0-f0e54357d8f0
topic_type:
- apiref
ms.openlocfilehash: d6ba0d073e8807ac6173f7f3e3982fe1d3eb4e01
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791433"
---
# <a name="icordebugilframecansetip-method"></a>Método ICorDebugILFrame::CanSetIP

Obtém um HRESULT que indica se é seguro definir o ponteiro de instrução para o local de deslocamento especificado no código MSIL (Microsoft Intermediate Language).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CanSetIP (  
    [in] ULONG32   nOffset  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `nOffset`  
 no A configuração desejada para o ponteiro de instrução.  
  
## <a name="remarks"></a>Comentários  

 Use o `CanSetIP` método antes de chamar o método [ICorDebugILFrame:: SetIP](icordebugilframe-setip-method.md) . Se `CanSetIP` o retornar qualquer HRESULT diferente de S_OK, você ainda poderá invocar `ICorDebugILFrame::SetIP` , mas não há nenhuma garantia de que o depurador continuará a execução segura e correta do código que está sendo depurado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug. idl, CorDebug, h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
