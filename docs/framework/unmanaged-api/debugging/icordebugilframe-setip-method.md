---
description: 'Saiba mais sobre: ICorDebugILFrame:: método SetIP'
title: Método ICorDebugILFrame::SetIP
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.SetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::SetIP
helpviewer_keywords:
- SetIP method, ICorDebugILFrame interface [.NET Framework debugging]
- ICorDebugILFrame::SetIP method [.NET Framework debugging]
ms.assetid: 23f38dc1-85e4-4263-9235-2d05bbb6a833
topic_type:
- apiref
ms.openlocfilehash: 75d2530a3d9151c64980316757074141776a78d3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791316"
---
# <a name="icordebugilframesetip-method"></a>Método ICorDebugILFrame::SetIP

Define o ponteiro de instrução para o local de deslocamento especificado no código MSIL (Microsoft Intermediate Language).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetIP (  
    [in] ULONG32 nOffset  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `nOffset`  
 O local de deslocamento no código MSIL.  
  
## <a name="remarks"></a>Comentários  

 As chamadas para `SetIP` invalidar imediatamente todos os quadros e cadeias para o thread atual. Se o depurador precisar de informações de quadro após uma chamada para `SetIP` , ele deverá executar um novo rastreamento de pilha.  
  
 [ICorDebug](icordebug-interface.md) tentará manter o quadro de pilha em um estado válido. No entanto, mesmo que o quadro esteja em um estado válido, ainda pode haver problemas como variáveis locais não inicializadas. O chamador é responsável por garantir a coerência do programa em execução.  
  
 Em plataformas de 64 bits, o ponteiro de instrução não pode ser movido para fora de um `catch` `finally` bloco ou. Se `SetIP` for chamado para fazer uma movimentação desse tipo em uma plataforma de 64 bits, ele retornará um HRESULT indicando falha.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
