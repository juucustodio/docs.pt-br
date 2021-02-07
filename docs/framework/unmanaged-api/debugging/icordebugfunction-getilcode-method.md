---
description: 'Saiba mais sobre o método: ICorDebugFunction:: GetILCode'
title: Método ICorDebugFunction::GetILCode
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetILCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetILCode
helpviewer_keywords:
- ICorDebugFunction::GetILCode method [.NET Framework debugging]
- GetILCode method [.NET Framework debugging]
ms.assetid: f794dd47-a7cd-47f6-96e9-a41a4dae8e72
topic_type:
- apiref
ms.openlocfilehash: 3b7bb29a028b189b24d3fbf02edc8190d9989a51
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692518"
---
# <a name="icordebugfunctiongetilcode-method"></a>Método ICorDebugFunction::GetILCode

Obtém a instância ICorDebugCode que representa o código MSIL (Microsoft Intermediate Language) associado a este objeto ICorDebugFunction.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetILCode (  
    [out] ICorDebugCode **ppCode  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppCode`  
 fora Um ponteiro para a `ICorDebugCode` instância, ou NULL, se a função não foi compilada em MSIL.  
  
## <a name="remarks"></a>Comentários  

 Se editar e continuar tiver sido permitido nessa função, o `GetILCode` método obterá o código MSIL correspondente à versão editada da função do código no Common Language Runtime (CLR).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
