---
description: 'Saiba mais sobre o método: ICorDebugILFrame:: EnumerateLocalVariables'
title: Método ICorDebugILFrame::EnumerateLocalVariables
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.EnumerateLocalVariables
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::EnumerateLocalVariables
helpviewer_keywords:
- EnumerateLocalVariables method [.NET Framework debugging]
- ICorDebugILFrame::EnumerateLocalVariables method [.NET Framework debugging]
ms.assetid: 1a67fa1b-2419-4cd0-aad4-6f46a0719b4b
topic_type:
- apiref
ms.openlocfilehash: 275cf7fcad32c452e6e7ebdd0774d64708a2398c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791381"
---
# <a name="icordebugilframeenumeratelocalvariables-method"></a>Método ICorDebugILFrame::EnumerateLocalVariables

Obtém um enumerador para as variáveis locais neste quadro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateLocalVariables(
    [out] ICorDebugValueEnum    **ppValueEnum  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppValueEnum`  
 [out] Um ponteiro para o endereço de um objeto ICorDebugValueEnum que é o enumerador das variáveis locais neste quadro.  
  
## <a name="remarks"></a>Comentários  

 `EnumerateLocalVariables` Obtém um enumerador que pode listar as variáveis locais disponíveis no quadro de chamada que é representado por esse objeto ICorDebugILFrame. A lista pode não incluir todas as variáveis locais na função em execução, pois algumas delas podem não estar ativas.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
