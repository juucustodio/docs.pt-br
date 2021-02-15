---
description: 'Saiba mais sobre o método: ICorDebugFunction:: GetNativeCode'
title: Método ICorDebugFunction::GetNativeCode
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetNativeCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetNativeCode
helpviewer_keywords:
- GetNativeCode method [.NET Framework debugging]
- ICorDebugFunction::GetNativeCode method [.NET Framework debugging]
ms.assetid: c8a34916-0eef-4987-8d29-c8bcb4be9cf6
topic_type:
- apiref
ms.openlocfilehash: 8938e11a5fdc3aa693faf04eec639941475d95ac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692440"
---
# <a name="icordebugfunctiongetnativecode-method"></a>Método ICorDebugFunction::GetNativeCode

Obtém o código nativo para a função que é representada por essa instância de ICorDebugFunction.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetNativeCode (  
    [out] ICorDebugCode **ppCode  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppCode`  
 fora Um ponteiro para a instância ICorDebugCode que representa o código nativo para essa função, ou NULL, se essa função for um código MSIL (Microsoft Intermediate Language) que não tenha sido compilado JIT (just-in-time).  
  
## <a name="remarks"></a>Comentários  

 Se a função representada por essa `ICorDebugFunction` instância tiver sido compilada por JIT mais de uma vez, como no caso de tipos genéricos, `GetNativeCode` o retornará um objeto de código nativo aleatório.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
