---
description: 'Saiba mais sobre o método: ICorDebugStepper:: SetInterceptMask'
title: Método ICorDebugStepper::SetInterceptMask
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.SetInterceptMask
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::SetInterceptMask
helpviewer_keywords:
- SetInterceptMask method [.NET Framework debugging]
- ICorDebugStepper::SetInterceptMask method [.NET Framework debugging]
ms.assetid: 6245e2ae-5cc2-43ff-8cc1-71953d12113a
topic_type:
- apiref
ms.openlocfilehash: 33a42b154d063a29022034fd8061599a5e0e5503
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803536"
---
# <a name="icordebugsteppersetinterceptmask-method"></a>Método ICorDebugStepper::SetInterceptMask

Define um valor que especifica os tipos de código que são percorridos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetInterceptMask (  
    [in] CorDebugIntercept    mask  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `mask`  
 no Uma combinação de valores da enumeração CorDebugIntercept que especifica os tipos de código.  
  
## <a name="remarks"></a>Comentários  

 Se o bit de um interceptor for definido, o stepper será concluído quando o tipo de código de interceptação for encontrado. Se o bit for apagado, o código de interceptação será ignorado.  
  
 O `SetInterceptMask` método pode ter interações imprevistas com [ICorDebugStepper:: SetUnmappedStopMask](icordebugstepper-setunmappedstopmask-method.md) (do ponto de vista do usuário). Por exemplo, se a única parte visível (ou seja, não interna) do código de inicialização da classe não tiver informações de mapeamento e STOP_NO_MAPPING_INFO não estiver definida (consulte o método [ICorDebugStepper:: SetUnmappedStopMask](icordebugstepper-setunmappedstopmask-method.md) e a Enumeração CorDebugUnmappedStop), o stepper passará pela inicialização da classe. Por padrão, somente o valor INTERCEPT_NONE da `CorDebugIntercept` Enumeração será usado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
