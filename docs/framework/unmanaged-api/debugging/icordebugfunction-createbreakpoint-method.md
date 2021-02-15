---
description: 'Saiba mais sobre o método: ICorDebugFunction:: CreateBreakpoint'
title: Método ICorDebugFunction::CreateBreakpoint
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.CreateBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::CreateBreakpoint
helpviewer_keywords:
- ICorDebugFunction::CreateBreakpoint method [.NET Framework debugging]
- CreateBreakpoint method, ICorDebugFunction interface [.NET Framework debugging]
ms.assetid: ffd0f708-0d21-4fae-a395-63b6c45828fa
topic_type:
- apiref
ms.openlocfilehash: 4d55a818352ff98b67c95d5ef15417f2e9e64d40
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692609"
---
# <a name="icordebugfunctioncreatebreakpoint-method"></a>Método ICorDebugFunction::CreateBreakpoint

Cria um ponto de interrupção no início desta função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateBreakpoint (  
    [out] ICorDebugFunctionBreakpoint **ppBreakpoint  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppBreakpoint`  
 fora Um ponteiro para o endereço de um objeto ICorDebugFunctionBreakpoint que representa o novo ponto de interrupção para a função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
